---
title: 通过SSH通道连接PostgreSQL
description: 了解如何将PostgreSQL数据库连接到 [!DNL MBI] 通过SSH通道。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Connect `PostgreSQL` via `SSH` 隧道

连接您的 `PostgreSQL` 数据库至 [!DNL MBI] 通过 `SSH tunnel`，您（或您的团队，如果您不是技术人员）必须执行以下操作：

1. [检索 [!DNL MBI] 公钥](#retrieve)
1. [允许访问 [!DNL MBI] IP地址](#allowlist)
1. [创建Linux](#linux)
1. [为创建Postgres用户 [!DNL MBI] ](#postgres)
1. [在MBI中输入连接和用户信息](#finish)

它不像听起来那么复杂。 开始使用。

## 正在检索 [!DNL MBI] `public key` {#retrieve}

此 `public key` 用于授权 [!DNL MBI] Linux®用户。 在下一部分中，您将创建用户并导入密钥。

1. 转到 **[!UICONTROL Manage Data** > **Connections]** 并单击 **[!UICONTROL Add a Data Source]**.
1. 单击 `PostgreSQL` 图标。
1. 在 `PostgreSQL credentials` 页面打开，设置 `Encrypted` 切换到 `Yes`. 这会显示 `SSH` 设置表单。
1. 此 `public key` 位于此表单下。

在整个教程中保持此页面处于打开状态 — 您需要在下一部分和结尾处打开此页面。

如果您有点迷路，以下说明如何浏览 [!DNL MBI] 要检索密钥，请执行以下操作：

![检索RJMetrics公钥](../../../assets/get-mbi-public-key.gif)

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它是 `54.88.76.97/32`，但它也位于 `PostgreSQL` “身份证明”页。 看到上面GIF中的蓝框了吗？ 就是这样！

## 创建 `Linux` 用户 [!DNL MBI] {#linux}

这可以是生产或辅助计算机，只要它包含实时（或经常更新）数据即可。 您可以 [限制此用户](../../../administrator/account-management/restrict-db-access.md) 任何您喜欢的方式，只要它保留连接到PostgreSQL服务器的权限。

1. 要添加新用户，请以root用户身份在 `Linux` 服务器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 记住 `public key` 你是在第一节中找回的吗？ 要确保用户有权访问数据库，您需要将密钥导入 `authorized\_keys`.

   将整个密钥复制到 `authorized\_keys` 文件如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 要完成创建用户，请更改以下项的权限： `/home/rjmetric` 允许通过以下方式访问的目录 `SSH`：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 与服务器关联的文件未设置为默认选项，仅某些用户具有服务器访问权限 — 这会阻止成功连接到 [!DNL MBI]. 在这些情况下，必须运行命令，例如 `AllowUsers` 以允许rjmetric用户访问服务器。

## 创建 [!DNL MBI] Postgres用户 {#postgres}

您的组织可能需要不同的流程，但创建此用户的最简单方法是在以有权授予权限的用户身份登录Postgres时执行以下查询。 用户还应该拥有具有以下特征的架构： [!DNL MBI] 已被授予访问权限。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Replace `secure password` 使用您自己的安全密码，该密码可以与SSH密码不同。 此外，请确保将 `database name` 和 `schema name` 数据库中具有相应名称的用户名。

如果要连接多个数据库或架构，请根据需要重复此过程。

## 将连接和用户信息输入到 [!DNL MBI] {#finish}

要完成这些操作，您需要将连接和用户信息输入到 [!DNL MBI]. 是否保持打开PostgreSQL凭据页面？ 如果不能，请转到 **[!UICONTROL Manage Data > Connections]** 并单击 **[!UICONTROL Add a Data Source]**，然后单击PostgreSQL图标。 不要忘记设置 `Encrypted` 切换到 `Yes`.

从“数据库连接”部分开始，在此页中输入以下信息：

* `Username`： RJMetrics Postgres用户名（应为rjmetric）
* `Password`：RJMetrics Postgres密码
* `Port`：服务器上的PostgreSQL端口（默认为5432）
* `Host`: 127.0.0.1

下 `SSH Connection`：

* `Remote Address`：要通过SSH连接的服务器的IP地址或主机名
* `Username`：您的SSH登录名（应为rjmetric）
* `SSH Port`：服务器上的SSH端口（默认为22）

就是这样！ 完成后，单击 **保存并测试** 以完成设置。

### 相关

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
