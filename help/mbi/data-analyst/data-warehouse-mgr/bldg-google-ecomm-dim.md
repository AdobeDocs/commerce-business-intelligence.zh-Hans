---
title: 建置[!DNL Google ECommerce]維度
description: 瞭解如何建立將電子商務資料與訂單和客戶資料連結的維度。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 建置 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>需要 [管理員許可權](../../administrator/user-management/user-management.md).

現在您已完成 [連線您的[!DNL Google ECommerce] 帳戶](../../data-analyst/importing-data/integrations/google-ecommerce.md)，您能如何處理這些資料？ [!DNL Commerce Intelligence]？ 本主題將引導您建立維度，將您的電子商務資料與您的訂單和客戶資料連結。

所涵蓋的維度可讓您建置分析 [回答有關行銷管道和行銷活動的重要問題](../../data-analyst/analysis/most-value-source-channel.md). 每個來源佔收入的百分比為何？ 的期限值如何 [!DNL Facebook] 已獲得客戶與來自的客戶比較 [!DNL Google]？

## 必要條件和概觀

若要在此主題中建立維度，您需要 [!DNL Google ECommerce] 表格， an `orders` 表格和 `customers` 表格。 這些表格必須 [已同步至您的Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 建立維度之前。 已同步的表格會顯示在 `Synced Tables` 部分 `Data Warehouse Manager`.

如果您需要重新整理程式，以下提供同步表格和欄的快速檢視：

![](../../assets/Syncing_New_Columns.gif)

從建立聯結之後 `orders` 表格至 [!DNL Google eCommerce] 表格中，您會建立下列清單中的前三個維度。 接下來，您使用這些維度，在 `customers` 表格。 若要完成，請將這些欄聯結到 `orders` 表格。

以下是涵蓋的維度：

* **訂單表格**

* 訂單的 [!DNL Google Analytics] source
* 訂單的 [!DNL Google Analytics] 中
* 訂單的 [!DNL Google Analytics]行銷活動
* 客戶的第一筆訂單 [!DNL Google Analytics] source
* 客戶的第一筆訂單 [!DNL Google Analytics] 中
* 客戶的第一筆訂單 [!DNL Google Analytics] 行銷活動

* **Customers表格**

* 客戶的第一筆訂單 [!DNL Google Analytics] source
* 客戶的第一筆訂單 [!DNL Google Analytics] 中
* 客戶的第一筆訂單 [!DNL Google Analytics] 行銷活動

## 建立維度

若要建立尺寸，請開啟 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md) 按一下 **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 訂單表格，第1回合

此範例會建置 **訂單的 [!DNL Google Analytics] 來源** 維度。

1. 從Data Warehouse中的表格清單中，按一下表格(在此案例中， `orders`)，其中包含您的訂單資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 選取 `Joined Column` 從 [定義下拉式清單](../data-warehouse-mgr/calc-column-types.md). 此範例適用於 [一對一關係](../data-warehouse-mgr/table-relationships.md)，比對 `eCommerce.transactionID` 欄中的唯一一列 `orders` 表格。
1. 接下來，您需要定義路徑，或定義所使用的表格和欄的連線方式。 按一下 `Select a table and column` 下拉式清單。
1. 您需要的路徑無法使用，因此您需要建立新的路徑。 按一下 **[!UICONTROL Create new Path]**.
1. 在顯示的視窗中，設定 `Many` 側邊到 `orders.order\_id`，或中的欄 `orders` 包含訂單ID的表格。
1. 於 `One` 側，尋找 `Google ECommerce` 表格，然後將欄設定為 `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 按一下 **[!UICONTROL Save]** 以建立路徑。
1. 新增路徑後，按一下 **[!UICONTROL Select table and column]** 再下拉式清單。
1. 找到 `ECommerce` 表格，然後按一下 `Source` 欄。 這會將訂單與來源資訊繫結。
1. 回到表格結構描述後，請按一下 **[!UICONTROL Save]** 再次建立維度。

以下是整個程式的概況：

![](../../assets/help_center.gif)

接下來，嘗試建立 **訂單的 [!DNL Google Analytics] 中** 和 `campaign`. 這些維度沒有太多變更，所以請再試一次。 但如果您卡住了，可以結帳檢視 [本文結尾](#stuck) 以檢視不同之處。

### Customers表格 {#customers}

此範例會建置 **客戶的第一筆訂單 [!DNL Google Analytics] source** 維度。

1. 從Data Warehouse中的表格清單中，按一下表格(在此案例中， `customers`)，其中包含您的客戶資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 在此範例中，選取 `is MAX` 定義 [定義下拉式清單](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 此 `is MIN` 定義也可以套用至只有一個可能值的文字欄。 重要部分是確保設定正確的篩選器，稍後再執行。
1. 按一下 **[!UICONTROL Select a table and column]** 下拉式清單並選取 `orders` 表格，然後 `Order's [!DNL Google Analytics] source` 欄。
1. 按一下 **[!UICONTROL Save]**.
1. 回到表格結構描述後，按一下 `Options` 下拉式清單，然後 `Filters`.
1. 按一下 **[!UICONTROL Add Filter Set]** 然後選取 `Orders we count` 設定。 您只希望納入您盤點篩選集之訂單中的訂單，因此請務必選取此篩選集。
1. 按一下 **[!UICONTROL Add Filter]**. 您要尋找客戶的第一筆訂單 [!DNL Google Analytics] 來源，因此您需要新增篩選器：

   _orders.客戶的訂單編號= 1

   _
1. 按一下 **[!UICONTROL Save]** 以建立維度。

接下來，嘗試建立 **客戶的第一筆訂單 [!DNL Google Analytics] 中** 和 `campaign`. 這些維度沒有太多變更，所以請再試一次。 但如果您卡住了，可以結帳檢視 [本文結尾](#stuck) 以檢視不同之處。

### 額外優點：訂單表格，第2回合

如有需要，您可以在此停止，但本節可讓您透過以下專案來啟用進一步分析： **客戶的第一筆訂單 [!DNL Google Analytics] 維度** 您建立於 [最後一節](#customers) 到 `orders` 表格。 在此區段中建立維度可讓您分析以下專案上建立的所有量度： `orders` 表格 —  `Revenue`， `Number of orders`， `Distinct buyers`，等等 — 使用 [!DNL Google Analytics] 客戶第一筆訂單的屬性。

此範例會加入 `Customer's first order's [!DNL Google Analytics] source` 的維度 `orders` 表格。

1. 從Data Warehouse中的表格清單中，按一下表格(在此案例中， `orders`)，其中包含您的訂單資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 選取 `Joined Column` 從定義下拉式清單。 這會將您在上一節建立的客戶維度加入 `orders` 表格。
1. 按一下 **[!UICONTROL Select a table and column]** 下拉式清單，然後選取 `customers` 表格和 `Customer's first order's [!DNL Google Analytics] source` 欄。
1. 如果路徑未自動填入，請選取最能連線客戶與訂單表格的路徑。
1. 按一下 **[!UICONTROL Save]** 以建立維度。

以下是整個程式的概況：

![](../../assets/help_center2.gif)

加入 `Customer's first order's` 中和 `campaign` 的維度 `orders` 表格。 加入維度，如果發生問題，則出庫 [文章結尾](#stuck) 如果您需要協助。

### 正在結束

您已建立完維度，這表示您現在可以建立強大的分析來追蹤各種管道和行銷活動的績效。 請記住 **新欄要等到下一次更新完成後才能使用**.

本主題會介紹一些較受歡迎的維度，但天空是限制 — 請嘗試建立您自己的維度，或如果您想尋求探索其他選項的協助，請隨時向我們撥打電話。 

### 其他附註

**`Orders`表格#1**：建立時 `Order's [!DNL Google Analytics]` 中和 `campaign` 尺寸不同，差異在於步驟12中選取的欄。 在此範例中，欄是 `Source`.

**`Customers`表格**：建立時 `Customer's first order's [!DNL Google Analytics]` 中和 `campaign` 尺寸不同，差異在於步驟5中選取的欄。 在此範例中，欄是 `Order's [!DNL Google Analytics]` 來源。

**`Orders`表格#2**：加入 `Customer's first order's [!DNL Google Analytics]` 中和 `campaign` 欄至 `orders` 表格中，差異為步驟5中所選取的欄。 在此範例中，欄是 `Customer's first order's [!DNL Google Analytics]` 來源。
