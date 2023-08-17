---
title: 通过直接连接连接MySQL
description: 了解如何连接 [!DNL MongoDB] 通过直接连接。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 连接 [!DNL MySQL] 通过直接连接

## 在本主题中

* [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
* [创建 [!DNL MySQL] 用户用于 [!DNL Commerce Intelligence]](#steptwo)
* [将连接信息输入到 [!DNL Commerce Intelligence]](#stepthree)

## 跳转到

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] 建议您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或其他形式的加密来保护您的数据！ 如果此选项不可用，您仍可以直接连接 [!DNL Commerce Intelligence] 使用本主题中的说明访问数据库。

本主题将指导您直接连接 [!DNL MySQL] 数据库至 [!DNL Commerce Intelligence]. 这些设置也可以与 [!DNL Adobe Commerce] 或任何其他使用MySQL的电子商务数据库。

## 允许访问 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 他们是 `54.88.76.97` 和 `34.250.211.151`，但它也位于 [!DNL MySQL] “身份证明”页：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 创建 [!DNL MySQL] 用户用于 [!DNL Commerce Intelligence]

创建的最简单方法 `MySQL` 用户用于 [!DNL Commerce Intelligence] 表示在登录时执行以下查询 `MySQL` 替换为 `GRANT` 权限。 替换 `Commerce Intelligence IP Address` 使用 [!DNL Commerce Intelligence] IP地址和替换 `secure password` 为您选择的安全密码：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行 `GRANT` 仅允许访问您允许的数据的查询。

**使用相同的用户和密码为所有必需的IP重新运行GRANT查询。**

## 在Commerce Intelligence中输入连接信息

要完成这些工作，您需要将连接和用户信息输入到 [!DNL Commerce Intelligence]. 你离开了 [!DNL MySQL] 凭据页面是否打开？ 如果没有，请转到 **[!UICONTROL Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，然后单击 [!DNL MySQL] 图标。 不要忘记更改 `Encrypted` 切换到 `Yes`.

在此页面中输入以下信息，从 `Database Connection` 部分：

* `Connection Nickname`：输入集成的名称（例如，电子商务商店）
* `Username`：的用户名 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Password`：的密码 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Port`：服务器上的MySQL端口(`3306` 默认)
* `Host`：默认情况下，这是localhost。 通常，它是的绑定地址值 [!DNL MySQL] 服务器，默认情况下为 `127.0.0.1 (localhost)`，但也可能是一些本地网络地址(例如， `192.168.0.1`)或服务器的公共IP地址。

  该值可在以下位置找到： `my.cnf` 文件(位于 `/etc/my.cnf`)下，代码为 `\[mysqld\]`. 如果bind-address行在该文件中被注释掉，则您的服务器将免受外部连接尝试的保护。

完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关文档

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
