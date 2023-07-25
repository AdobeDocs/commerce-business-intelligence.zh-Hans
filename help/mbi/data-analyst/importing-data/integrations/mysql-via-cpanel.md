---
title: 通过cPanel连接MySQL
description: 了解如何通过cPanel连接MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Connect [!DNL MySQL] via [!DNL cPanel]

* [创建 [!DNL Commerce Intelligence] [!DNL MySQL] 用户位置 [!DNL cPanel]](#cpanel)
* [将连接和用户信息输入到 [!DNL Commerce Intelligence]](#finish)

## 跳转到

* [[!DNL MySQL] 通过SSH通道](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 通过直接连接](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] 建议您使用SSH或其他某种加密形式来保护您的数据！ 如果此选项不可用，您仍可以直接连接 [!DNL Commerce Intelligence] 使用本主题中的说明访问数据库。

本主题将指导您完成直接连接 [!DNL MySQL] 数据库至 [!DNL Commerce Intelligence] 使用 [!DNL cPanel]. 此进程也可用于连接 [!DNL Adobe Commerce] 和任何其他基于MySQL的电子商务数据库 [!DNL Commerce Intelligence].

1. 创建 [!DNL Commerce Intelligence] [!DNL MySQL] 用户位置 [!DNL cPanel]
1. 将连接和用户信息输入到 [!DNL Commerce Intelligence]

开始使用。

## 创建 [!DNL Commerce Intelligence] [!DNL MySQL] 用户位置 [!DNL cPanel] {#cpanel}

1. 登录 [!DNL cPanel] 通过您的托管提供商。
1. 单击 **[!UICONTROL [!DNL MySQL] Databases]**，位于 `Database` 部分。
1. 向下滚动到 `Add New User` 部分和创建用户 [!DNL Commerce Intelligence]：

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 单击 **[!UICONTROL Create User]**.
1. 现在您已经创建了用户，您需要将其关联到数据库。 返回至 `Add New User` 部分 — 查看设置 `Add User to Database?` 那是你所需要的。
1. 在 `User` 在此部分的下拉列表中，选择您创建的用户。
1. 在 `Database` 在此部分的下拉列表中，选择要连接的数据库 [!DNL Commerce Intelligence].
1. 单击 **[!UICONTROL Add]**.
1. 出现权限核对清单时，选中旁边的复选框 `SELECT`  — 仅此而已 [!DNL Commerce Intelligence] 需要连接到数据库。

## 将连接和用户信息输入到 [!DNL Commerce Intelligence] {#finish}

要完成这些操作，您需要将连接和用户信息输入到 [!DNL Commerce Intelligence]. 您是否离开了 [!DNL MySQL] 凭据页面是否打开？ 如果不能，请转到 **[!UICONTROL Manage Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，则 [!DNL MySQL] 图标。

将以下信息输入此页面的 `Database Connection` 部分：

* `Username`：的用户名 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Password`：的密码 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Port`：服务器上的MySQL端口(`3306` 默认)
* `Host`：的公共地址 `MySQL` 服务器 [!DNL Commerce Intelligence] 连接到。 这通常是您用来登录的URL `[!DNL cPanel]`.

如果您使用 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，则必须输入加密信息。 设置 `Encrypted` 切换到 `Yes` 以显示表单。

* `Connection Type`：将此项设置为 `SSH Tunnel`
* `Remote Address`：服务器的IP地址或主机名 [!DNL Commerce Intelligence] 将隧道连接至
* `Username`：的用户名 [!DNL Commerce Intelligence] `SSH (Linux)` 用户，请参见 [说明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 如何执行此操作（如果尚未完成）
* `SSH Port`：服务器上的SSH端口(`22` 默认)

完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关：

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
