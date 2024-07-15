---
title: 通过SSH通道连接PostgreSQL
description: 了解如何通过SSH通道将PostgreSQL数据库连接到Commerce Intelligence。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 通过[!DNL SSH Tunnel]连接[!DNL PostgreSQL]

要通过`SSH tunnel`将您的[!DNL PostgreSQL]数据库连接到[!DNL Commerce Intelligence]，您必须执行以下操作：

1. [检索 [!DNL Commerce Intelligence] 公钥](#retrieve)
1. [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [为 [!DNL Commerce Intelligence]创建 [!DNL Linux] 用户](#linux)
1. [为 [!DNL Commerce Intelligence]创建 [!DNL PostgreSQL] 用户](#postgres)
1. [在 [!DNL Commerce Intelligence]中输入连接和用户信息](#finish)

## 正在检索[!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

`public key`用于授权[!DNL Commerce Intelligence] [!DNL Linux]用户。 现在，您将创建用户并导入密钥。

1. 转到&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add a Data Source]**。
1. 单击[!DNL PostgreSQL]图标。
1. 打开`PostgreSQL credentials`页面后，将`Encrypted`切换设置为`Yes`。 这会显示`SSH`设置表单。
1. `public key`位于此表单下。

在整个教程中保持此页面处于打开状态 — 您将在下一部分和结尾处找到它。

下面演示了如何浏览[!DNL Commerce Intelligence]以检索密钥：

![正在检索RJMetrics公钥](../../../assets/get-mbi-public-key.gif)

## 允许访问[!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它是`54.88.76.97/32`，但它也位于`PostgreSQL`凭据页面上。 请参阅上面GIF中的蓝色方框。

## 正在为[!DNL Commerce Intelligence]创建[!DNL Linux]用户 {#linux}

这可以是生产或辅助计算机，只要它包含实时（或经常更新）数据。 您可以按照您喜欢的方式[限制此用户](../../../administrator/account-management/restrict-db-access.md)，只要它保留连接到[!DNL PostgreSQL]服务器的权利即可。

1. 要添加新用户，请以root用户身份在[!DNL Linux]服务器上运行以下命令：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 是否记得在第一节中检索到的`public key`？ 为确保用户有权访问数据库，您需要将密钥导入`authorized\_keys`。

   按如下方式将整个密钥复制到`authorized\_keys`文件中：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 要完成创建用户，请更改`/home/rjmetric`目录上的权限以允许通过`SSH`进行访问：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>如果与服务器关联的`sshd\_config`文件未设置为默认选项，则只有某些用户具有服务器访问权限 — 这会阻止成功连接到[!DNL Commerce Intelligence]。 在这些情况下，需要运行诸如`AllowUsers`之类的命令以允许rjmetric用户访问服务器。

## 创建[!DNL Commerce Intelligence] [!DNL Postgres]用户 {#postgres}

您的组织可能需要不同的流程，但创建此用户的最简单方法是在以有权授予权限的用户身份登录Postgres时执行以下查询。 该用户还应该拥有[!DNL Commerce Intelligence]被授予访问权限的架构。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

将`secure password`替换为您自己的安全密码，该密码可以不同于SSH密码。 此外，请确保将`database name`和`schema name`替换为数据库中的相应名称。

如果要连接多个数据库或架构，请根据需要重复此过程。

## 在[!DNL Commerce Intelligence]中输入连接和用户信息 {#finish}

要完成工作，您需要在[!DNL Commerce Intelligence]中输入连接和用户信息。 您是否让[!DNL PostgreSQL]凭据页面保持打开状态？ 如果没有，请转到&#x200B;**[!UICONTROL Manage Data > Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add a Data Source]**，然后单击[!DNL PostgreSQL]图标。 别忘了将`Encrypted`切换设置为`Yes`。

在此页面中输入以下信息，从`Database Connection`部分开始：

* `Username`： RJMetrics Postgres用户名（应为rjmetric）
* `Password`： RJMetrics Postgres密码
* `Port`：您服务器上的PostgreSQL端口（默认为5432）
* `Host`： 127.0.0.1

在`SSH Connection`下：

* `Remote Address`：要通过SSH连接的服务器的IP地址或主机名
* `Username`：您的SSH登录名（应为rjmetric）
* `SSH Port`：服务器上的SSH端口（默认为22）

完成后，单击&#x200B;**保存并测试**&#x200B;以完成设置。

### 相关

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
