---
title: 通过直接连接连接MySQL
description: 了解如何通过直接连接来连接 [!DNL MongoDB] 。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 通过直接连接连接[!DNL MySQL]

## 在本主题中

* [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
* [为 [!DNL MySQL] 创建 [!DNL Commerce Intelligence]用户](#steptwo)
* [在 [!DNL Commerce Intelligence]中输入连接信息](#stepthree)

## 跳转到

* [[!DNL MySQL]通过 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]通过 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe]建议您使用[SSH](../integrations/mysql-via-ssh-tunnel.md)或其他某种加密形式来保护您的数据！ 如果此选项不可用，则仍可以使用本主题中的说明直接将[!DNL Commerce Intelligence]连接到数据库。

本主题将指导您直接将[!DNL MySQL]数据库连接到[!DNL Commerce Intelligence]。 这些设置也可以与[!DNL Adobe Commerce]或使用MySQL的任何其他电子商务数据库一起使用。

## 允许访问[!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是`54.88.76.97`和`34.250.211.151`，但它也位于[!DNL MySQL]凭据页面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 为[!DNL MySQL]创建一个[!DNL Commerce Intelligence]用户

为`MySQL`创建[!DNL Commerce Intelligence]用户的最简单方法是在登录具有`MySQL`权限的`GRANT`时执行以下查询。 将`Commerce Intelligence IP Address`替换为[!DNL Commerce Intelligence] IP地址，并将`secure password`替换为您选择的安全密码：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行`GRANT`查询，这些查询只允许访问您允许的数据。

**使用相同的用户和密码为所有必需的IP重新运行GRANT查询。**

## 在Commerce Intelligence中输入连接信息

要完成工作，您需要在[!DNL Commerce Intelligence]中输入连接和用户信息。 您是否让[!DNL MySQL]凭据页面保持打开状态？ 如果没有，请转到&#x200B;**[!UICONTROL Data** > **Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add New Data Source]**，然后单击[!DNL MySQL]图标。 别忘了将`Encrypted`切换更改为`Yes`。

在此页面中输入以下信息，从`Database Connection`部分开始：

* `Connection Nickname`：输入集成的名称（例如，电子商务商店）
* `Username`： [!DNL Commerce Intelligence] [!DNL MySQL]用户的用户名
* `Password`： [!DNL Commerce Intelligence] [!DNL MySQL]用户的密码
* `Port`：您的服务器上的MySQL端口（默认为`3306`）
* `Host`：默认情况下，这是本地主机。 通常，它是[!DNL MySQL]服务器的绑定地址值，默认情况下为`127.0.0.1 (localhost)`，但也可以是某些本地网络地址（例如，`192.168.0.1`）或服务器的公共IP地址。

  该值可以在`my.cnf`文件（位于`/etc/my.cnf`）中读取`\[mysqld\]`的行下找到。 如果bind-address行在该文件中被注释掉，则您的服务器将免受外部连接尝试的保护。

完成后，单击&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成设置。

## 相关文档

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
