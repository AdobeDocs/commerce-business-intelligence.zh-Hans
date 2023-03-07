---
title: 通过直接连接连接MySQL
description: 了解如何连接 [!DNL MongoDB] 通过直接连接。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Connect [!DNL MongoDB] 通过直接连接

## 本文

* [允许访问 [!DNL MBI] IP地址](#allowlist)
* [创建 ](#steptwo)
* [将连接信息输入到 [!DNL MBI]](#stepthree)

## 跳转到

* [&#39;通过SSH通道的MySQL&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&#39;通过cPanel的MySQL&#39;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Adobe建议您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或其他形式的加密来保护您的数据！ 如果此选项不可用，您仍可以直接连接 [!DNL MBI] 使用本文中的说明访问数据库。

本文指导您将MySQL数据库直接连接到 [!DNL MBI]. 这些设置还可以与Commerce或使用MySQL的任何其他电子商务数据库一起使用。

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是 `54.88.76.97` 和 `34.250.211.151`，但它也位于MySQL凭据页面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 为创建MySQL用户 [!DNL MBI]

创建的最简单方法 `MySQL` 用户 [!DNL MBI] 是在登录时执行以下查询 `MySQL` 替换为 `GRANT` 权限。 Replace `MBI IP Address` 使用 [!DNL MBI] IP地址和替换 `secure password` 提供您选择的安全密码：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行 `GRANT` 仅允许访问您允许的数据的查询。

**使用相同的用户和密码为所有必需的IP重新运行GRANT查询。**

## 在MBI中输入连接信息

要完成这些操作，您需要将连接和用户信息输入到 [!DNL MBI]. 您是否让MySQL凭据页面处于打开状态？ 如果不能，请转到 **[!UICONTROL Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，然后单击MySQL图标。 不要忘记更改 `Encrypted` 切换到 `Yes`.

在此页面中输入以下信息，从 `Database Connection` 部分：

* `Connection Nickname`：输入集成的名称（例如，电子商务商店）
* `Username`：的用户名 [!DNL MBI] MySQL用户
* `Password`：的密码 [!DNL MBI] MySQL用户
* `Port`：服务器上的MySQL端口(`3306` 默认)
* `Host`：默认情况下，这是localhost。 通常，它是MySQL服务器的绑定地址值，默认情况下为 `127.0.0.1 (localhost)`，但也可以是某个本地网络地址(例如， `192.168.0.1`)或服务器的公共IP地址。

   该值可在以下位置找到： `my.cnf` 文件(位于 `/etc/my.cnf`)下，代码为 `\[mysqld\]`. 如果bind-address行在该文件中被注释掉，则您的服务器不会受到外部连接尝试的保护。

就是这样！ 完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关文档

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
