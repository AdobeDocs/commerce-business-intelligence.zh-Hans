---
title: 透過VPN連線資料庫
description: 瞭解如何透過VPN而非SSH通道連線資料庫。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 透過VPN連線資料庫

雖然Adobe建議您使用 `SSH tunnel`，您也可以使用加密的 `VPN` 連線以保障安全。 A `VPN` 可用於任何資料庫整合，而且為了簡化程式，此程式與設定 `SSH tunnel`：

1. [ [!DNL Commerce Intelligence] 创建数据库用户](#database)
1. [ [!DNL Commerce Intelligence] 创建 VPN 用户](#vpn)
1. [允许访问  [!DNL Commerce Intelligence]  IP 地址](#allowlist)
1. [将连接和 VPN 用户信息输入到商务智能中](#finish)

除了数据库凭据之外，您还必须输入 VPN 用户的凭据，以将内容包装。 任何 VPN 用户都能正常工作，但 Adobe Systems 建议您创建 [!DNL Commerce Intelligence] 用户，因为它可以更轻松地跟踪您帐户上的用户。

## 创建数据库用户 [!DNL Commerce Intelligence] {#database}

建立資料庫使用者的程式會依您連線的資料庫型別而有所不同。 若要檢視每種資料庫型別的指示，請按一下下列連結。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## `VPN`创建用户[!DNL Commerce Intelligence] {#vpn}

如前所述，任何有效 `VPN` 的用户都能起作用-但 Adobe Systems 建议您创建一个仅供使用的 [!DNL Commerce Intelligence] 用户。

## 允许访问 [!DNL Commerce Intelligence] IP 地址 {#allowlist}

要使连接成功，您必须配置防火墙以允许来自您的 IP 地址的访问。 它们也包括 `54.88.76.97` `34.250.211.151` 在任何数据库集成的 `credentials` 页面中：

![MBI_Allow_Access_IPs .png](../../../assets/MBI_allow_access_IPs.png)

## 輸入連線和 `VPN` 使用者資訊到 [!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須將連線和使用者資訊輸入到 [!DNL Commerce Intelligence]. 您是否離開資料庫 `credentials` 頁面是否開啟？ 如果沒有，請前往 **[!UICONTROL Manage Data** > **Connections]**. 按一下 **[!UICONTROL Add New Data Source]**，然後按一下要連線之資料庫的圖示。 別忘了變更 `Encrypted` 切換至 `Yes`.

在此頁面中輸入下列資訊，從 `Database Connection` 區段：

* `Username`：数据库的用户名 [!DNL Commerce Intelligence] 用户
* `Password`：数据库的密码 [!DNL Commerce Intelligence] 用户
* `Port`：数据库在您的服务器上的端口。 默认值为：
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`：預設為localhost `127.0.0.1`，但也可能是伺服器的公用IP位址或區域網路位址。
* `Database Name (optional)`：如果您只允許存取一個資料庫（這在資料庫使用者建立步驟中指定），請在此處輸入該資料庫的名稱。

在 `Encryption Connection` 區段：

* `Encryption Type`：将此设置为 `Cisco IPsec VPN`
* `Gateway Address`： VPN 服务器的 IP 地址
* `Group Name`：用于群组身份验证的群组的名称
* `Group Secret`：与群组对应的密码。
* `Username`[!DNL Commerce Intelligence] `VPN` ：用户名
* `Password`[!DNL Commerce Intelligence] `VPN` ：用户密码

完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。
