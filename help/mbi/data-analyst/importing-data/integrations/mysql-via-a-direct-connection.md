---
title: 通过直接连接连接MySQL
description: 了解如何连接 [!DNL MongoDB] 直接连接。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 连接 [!DNL MongoDB] 通过直接连接

## 在本文中

* [允许访问 [!DNL MBI] IP地址](#allowlist)
* [创建 ](#steptwo)
* [在 [!DNL MBI]](#stepthree)

## 跳到

* [“通过SSH隧道的MySQL”](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [“通过cPanel的MySQL”](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>我们强烈建议您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或其他加密方式来保护您的数据！ 如果不能，您仍然可以直接连接 [!DNL MBI] 使用本文中的说明将数据库添加到。

在本文中，我们将指导您直接将MySQL数据库连接到 [!DNL MBI]. 这些设置还可以与Commerce或使用MySQL的任何其他电子商务数据库一起使用。

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，您必须配置防火墙以允许从我们的IP地址访问。 是 `54.88.76.97` 和 `34.250.211.151`，但它也位于MySQL凭据页上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 为 [!DNL MBI]

创建 `MySQL` 用户 [!DNL MBI] 是在登录后执行以下查询 `MySQL` with `GRANT` 权限。 替换 `MBI IP Address` 和 [!DNL MBI] IP地址和替换 `secure password` 使用您选择的安全密码：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行 `GRANT` 仅允许访问您允许的数据的查询。

**使用相同的用户和密码为所有必需的IP重新运行GRANT查询。**

## 在MBI中输入连接信息

总结一下，我们需要在 [!DNL MBI]. 是否使MySQL凭据页保持打开状态？ 如果没有，请转到 **[!UICONTROL Data** > **Connections]** 单击 **[!UICONTROL Add New Data Source]**，然后显示MySQL图标。 不要忘记更改 `Encrypted` 切换至 `Yes`.

在此页面中输入以下信息(从 `Database Connection` 部分：

* `Connection Nickname`:输入集成的名称（例如，Ecommerce Store）
* `Username`:的用户名 [!DNL MBI] MySQL用户
* `Password`:的密码 [!DNL MBI] MySQL用户
* `Port`:您服务器上的MySQL端口(`3306` 默认)
* `Host`:默认情况下，这将为localhost。 通常，它将是MySQL服务器的绑定地址值，默认情况下为 `127.0.0.1 (localhost)`，但也可能是一些本地网络地址(例如， `192.168.0.1`)或您服务器的公共IP地址。

   值可在 `my.cnf` 文件(通常位于 `/etc/my.cnf`) `\[mysqld\]`. 如果绑定地址行在该文件中被注释掉，则服务器将受到外部连接尝试的保护。

就这样！ 完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关文档

* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
