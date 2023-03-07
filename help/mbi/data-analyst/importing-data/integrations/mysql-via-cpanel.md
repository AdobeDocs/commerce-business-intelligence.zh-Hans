---
title: 通过cPanel连接MySQL
description: 了解如何通过cPanel连接MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# 通过cPanel连接MySQL

* [创建 [!DNL MBI] cPanel中的MySQL用户](#cpanel)
* [在MBI中输入连接和用户信息](#finish)

## 跳转到

* [通过SSH通道的MySQL](../integrations/mysql-via-ssh-tunnel.md)
* [通过直接连接访问MySQL](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>Adobe建议您使用SSH或其他某种加密形式来保护您的数据！ 如果此选项不可用，您仍可以直接连接 [!DNL MBI] 使用本文中的说明访问数据库。

本文指导您将MySQL数据库直接连接到 [!DNL MBI] 使用 `cPanel`. 此进程也可用于连接 [!DNL Adobe Commerce] 和任何其他基于MySQL的电子商务数据库 [!DNL MBI].

1. 创建 [!DNL MBI] 中的MySQL用户 `cPanel`
1. 将连接和用户信息输入到 [!DNL MBI]

开始使用。

## 创建 [!DNL MBI] 中的MySQL用户 `cPanel` {#cpanel}

1. 登录 [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) 通过您的托管提供商。
1. 单击 **[!UICONTROL MySQL Databases]**，位于 `Database` 部分。
1. 向下滚动到 `Add New User` 部分和创建用户 [!DNL MBI]：

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 单击 **[!UICONTROL Create User]**.
1. 现在您已经创建了用户，您需要将其关联到数据库。 返回至 `Add New User` 部分 — 查看设置 `Add User to Database?` 那是你所需要的。
1. 在 `User` 在此部分的下拉列表中，选择您创建的用户。
1. 在 `Database` 在此部分的下拉列表中，选择要连接的数据库 [!DNL MBI].
1. 单击 **[!UICONTROL Add]**.
1. 出现权限核对清单时，选中旁边的复选框 `SELECT`  — 仅此而已 [!DNL MBI] 需要连接到数据库。

## 将连接和用户信息输入到 [!DNL MBI] {#finish}

要完成这些操作，您需要将连接和用户信息输入到 [!DNL MBI]. 您是否让MySQL凭据页面处于打开状态？ 如果不能，请转到 **[!UICONTROL Manage Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，然后单击MySQL图标。

将以下信息输入此页面的 `Database Connection` 部分：

* `Username`：的用户名 [!DNL MBI] MySQL用户
* `Password`：的密码 [!DNL MBI] MySQL用户
* `Port`：服务器上的MySQL端口(`3306` 默认)
* `Host`：的公共地址 `MySQL` 服务器 [!DNL MBI] 连接到。 这通常是您用来登录的URL `cPanel`.

如果您使用 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，则必须输入加密信息。 设置 `Encrypted` 切换到 `Yes` 以显示表单。

* `Connection Type`：将此项设置为 `SSH Tunnel`
* `Remote Address`：服务器的IP地址或主机名 [!DNL MBI] 将隧道连接至
* `Username`：的用户名 [!DNL MBI] `SSH (Linux)` 用户，请参见 [说明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 如何执行此操作（如果尚未完成）
* `SSH Port`：服务器上的SSH端口(`22` 默认)

就是这样！ 完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关：

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
