---
title: 通过cPanel连接MySQL
description: 了解如何通过cPanel连接MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 通过[!DNL MySQL]连接[!DNL cPanel]

* [在 [!DNL Commerce Intelligence] [!DNL MySQL]中创建 [!DNL cPanel]用户](#cpanel)
* [在 [!DNL Commerce Intelligence]中输入连接和用户信息](#finish)

## 跳转到

* [通过SSH通道的[!DNL MySQL]](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]通过直接连接](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe]建议您使用SSH或其他加密形式来保护您的数据！ 如果此选项不可用，则仍可以使用本主题中的说明直接将[!DNL Commerce Intelligence]连接到数据库。

本主题将指导您使用[!DNL MySQL]将[!DNL Commerce Intelligence]数据库直接连接到[!DNL cPanel]。 此进程还可用于将[!DNL Adobe Commerce]和任何其他基于MySQL的电子商务数据库连接到[!DNL Commerce Intelligence]。

1. 在[!DNL Commerce Intelligence]中创建[!DNL MySQL] [!DNL cPanel]用户
1. 在[!DNL Commerce Intelligence]中输入连接和用户信息

开始使用。

## 在[!DNL Commerce Intelligence]中创建[!DNL MySQL] [!DNL cPanel]用户 {#cpanel}

1. 通过您的托管提供商登录[!DNL cPanel]。
1. 单击&#x200B;**[!UICONTROL [!DNL MySQL] Databases]**&#x200B;部分中的`Database`。
1. 向下滚动到`Add New User`部分并为[!DNL Commerce Intelligence]创建用户：

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 单击&#x200B;**[!UICONTROL Create User]**。
1. 现在您已经创建了用户，您需要将其关联到数据库。 返回`Add New User`部分 — 查看`Add User to Database?`的设置。这是您所需要的。
1. 在此分区的`User`下拉列表中，选择您创建的用户。
1. 在此部分的`Database`下拉列表中，选择要连接到[!DNL Commerce Intelligence]的数据库。
1. 单击&#x200B;**[!UICONTROL Add]**。
1. 出现权限核对清单时，选中`SELECT`旁边的框 — 这是[!DNL Commerce Intelligence]连接到数据库所需的全部。

## 在[!DNL Commerce Intelligence]中输入连接和用户信息 {#finish}

要完成工作，您需要在[!DNL Commerce Intelligence]中输入连接和用户信息。 您是否让[!DNL MySQL]凭据页面保持打开状态？ 如果没有，请转到&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add New Data Source]**，然后单击[!DNL MySQL]图标。

在此页面的`Database Connection`部分输入以下信息：

* `Username`： [!DNL Commerce Intelligence] [!DNL MySQL]用户的用户名
* `Password`： [!DNL Commerce Intelligence] [!DNL MySQL]用户的密码
* `Port`：您的服务器上的MySQL端口（默认为`3306`）
* `Host`： `MySQL`服务器[!DNL Commerce Intelligence]所连接的公用地址。 这通常是您用于登录到`[!DNL cPanel]`的URL。

如果您使用的是[`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，则必须输入加密信息。 将`Encrypted`切换设置为`Yes`以显示表单。

* `Connection Type`：将此项设置为`SSH Tunnel`
* `Remote Address`：服务器[!DNL Commerce Intelligence]的IP地址或主机名将隧道到
* `Username`： [!DNL Commerce Intelligence] `SSH (Linux)`用户的用户名，请参阅[说明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)以了解如何执行此操作（如果尚未这样做）
* `SSH Port`：服务器上的SSH端口（默认为`22`）

完成后，单击&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成设置。

## 相关：

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
