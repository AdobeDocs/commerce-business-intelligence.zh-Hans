---
title: 連線Amazon RDS
description: 瞭解連線您的RDS執行個體的步驟。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Connect [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] 是在您可能已經熟悉的資料庫引擎上執行的Managed資料庫服務：

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

連線您的電腦的步驟 [!DNL RDS] 執行個體會依您使用的資料庫型別，以及您是否使用加密連線(例如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，以下是基本介紹。

## 授權 [!DNL Commerce Intelligence] 以存取您的資料庫

在認證頁面(**[!UICONTROL Manage Data** > **Integrations]**)對於每個資料庫，您會看到一個方塊，其中包含您必須授權才能連線的IP位址[!DNL RDS] 至 [!DNL Commerce Intelligence]： `54.88.76.97` 和 `34.250.211.151`. 以下為檢視 `MySQL credentials` 頁面中，您反白顯示IP位址方塊：

![](../../../assets/RDS_IP.png)

對象 [!DNL Commerce Intelligence] 以成功連線您的 [!DNL RDS] 執行個體時，您必須透過AWS管理主控台，將這些IP位址新增至適當的資料庫安全性群組。 這些IP位址可以新增至現有群組，或者您可以建立一個IP位址 — 重要的是，群組有權存取您要連線的執行個體 [!DNL Commerce Intelligence].

新增 [!DNL Commerce Intelligence] ip位址，請務必新增 `/32` 至地址結尾以表示 [!DNL Amazon] 表示它是確切的IP位址。 別擔心；AWS介面會明確指出這是必要專案。

## 建立 `Linux` 使用者 [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>只有在您使用加密連線時，才需要執行此步驟。 如需如何執行此動作的說明，請參閱您使用之資料庫的設定主題（例如：MySQL）。 此 `Linux` 使用者允許我們建立 `SSH tunnel`，這是透過網際網路傳送資料最安全的方法。

## 建立資料庫使用者 [!DNL Commerce Intelligence]

根據您使用的資料庫，步驟會有所不同。 不過，您的想法是一樣的，您會為以下專案建立使用者： [!DNL Commerce Intelligence] 用來存取您的資料庫。 建立資料庫的指示 [!DNL Commerce Intelligence] 使用者可在您使用之資料庫的設定主題中找到。

## 將連線資訊輸入到 [!DNL Commerce Intelligence]

在您授與之後 [!DNL Commerce Intelligence] 存取您的執行個體並建立了一個使用者，您最後需要做的就是將連線資訊輸入到 [!DNL Commerce Intelligence].

的認證頁面 `MySQL`， `Microsoft SQL`、和 `PostgreSQL` 可透過 `Integrations` 頁面(**[!UICONTROL Manage Data** > **Integrations]**)，方法是按一下 **[!UICONTROL Add Integration]**. 顯示整合清單時，按一下您用來移至「證明資料」頁面的資料庫圖示。 如果您目前無法存取所需的整合，請聯絡您的Adobe客戶團隊。

若要完成連線的建立，您需要下列資訊：

* 您的RDS執行個體的公用位址：這可以在 [!DNL AWS] 管理主控台。
* 資料庫執行處理使用的連線埠：有些資料庫有預設的連線埠，會自動填入 `Port` 欄位。 此資訊也可在資料庫的設定檔案中找到。
* 您為其建立之使用者的使用者名稱和密碼 [!DNL Commerce Intelligence].

如果您使用加密連線，請變更 `Encrypted` 將「資料庫證明資料」頁面切換為 `Yes`. 這會顯示一個額外表單來設定加密：

![](../../../assets/sql-integration-encrypted-yes.png)


