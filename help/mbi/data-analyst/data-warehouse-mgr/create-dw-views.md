---
title: 建立及使用Data Warehouse檢視
description: 瞭解藉由修改現有表格或使用SQL將多個表格聯結或合併在一起來建立新倉儲表格的方法。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# 使用Data Warehouse檢視

本檔案概述的用途與用途 `Data Warehouse Views` 可透過導覽至 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 以下說明其功用以及如何建立檢視，並舉例說明如何使用 `Data Warehouse Views` 合併 [!DNL Facebook] 和 [!DNL AdWords] 支出資料。

## 一般用途

此 `Data Warehouse Views` 功能是透過修改現有表格或使用SQL將多個表格聯結或合併在一起來建立新倉儲表格的方法。 一次a `Data Warehouse View` 已透過更新週期建立及處理，則會在Data Warehouse中填入新表格，位於 `Data Warehouse Views` 下拉式清單，如下所示：

![](../../assets/Data_Warehouse.png)

從此處，您的新檢視功能會與任何其他表格類似，讓您能夠建立新的計算欄，或在其上建立量度和報表。

`Data Warehouse Views` 主要用於合併多個相似但不同的表格，以便所有報表都建立在單一新表格上。 常見的範例包括合併舊版資料庫和即時資料庫的表格，以結合歷史資料和目前資料，或將多個廣告來源(例如Facebook和AdWords)合併為單一 `Consolidated ad spend` 表格。

如果您熟悉SQL，這兩個合併範例都會使用 `UNION` 函式，但您可在建立新檢視時使用任何PostgreSQL語法和函式。

## 建立和管理Data Warehouse檢視

新增 `Data Warehouse Views` 您可以導覽至「 」以建立及刪除現有檢視 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，如下所示：

![](../../assets/Data_Warehouse_Views.png)

您可以在此處依照下列範例指示建立檢視：

1. 如果觀察現有檢視，請按一下 **[!UICONTROL New Data Warehouse View]** 以開啟空白查詢視窗。 如果已經開啟空白查詢視窗，請繼續進行下一個步驟。
1. 輸入檢視的名稱 `View Name` 欄位。 此處提供的名稱會決定Data Warehouse中檢視的顯示名稱。 `View names` 僅限於小寫字母、數字和底線(_)。 禁止使用所有其他字元。
1. 在標題為的視窗中輸入查詢 `Select Query`，使用標準PostgreSQL語法。

   >[!NOTE]
   >
   >您的查詢必須參考特定的欄名稱。 使用 `*`不允許字元選取所有欄。

1. 完成後，按一下 **[!UICONTROL Save]** 以儲存您的檢視。 您的檢視暫時 `Pending` 狀態，直到下一次完整更新週期處理為止，此時狀態會變更為 `Active`. 更新處理完後，您的檢視即可在報告中使用。

請務必注意，在儲存後，用於產生 `Data Warehouse View` 無法編輯。 如果您需要調整的結構 `Data Warehouse View`，您必須建立檢視，並手動將任何計算欄、量度或報表從原始檢視移轉到新檢視。 移轉完成後，您可以安全地刪除原始檢視。 因為 `Data Warehouse Views` 不可編輯，Adobe建議您使用 `SQL Report Builder` 將查詢儲存為Data Warehouse檢視之前。

## 範例： [!DNL Facebook] 和 [!DNL Google AdWords] 資料

請仔細檢視本文前面提到的其中一個範例：合併 [!DNL Facebook] 和 [!DNL AdWords] 將資料放入新的整合式廣告表格中。 這通常涉及兩個表格的合併，範例資料集如下：

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

若要建立包含兩者的單一廣告支出表格 [!DNL Facebook] 和 [!DNL Google AdWords] 行銷活動，您必須撰寫SQL查詢並使用 `UNION ALL` 函式。 A `UNION ALL` 陳述式最常用來合併多個不同的SQL查詢，同時將每個查詢的結果附加至單一輸出。

有一些需求 `UNION` 值得一提的陳述式，如PostgreSQL中所述 [檔案](https://www.postgresql.org/docs/8.3/queries-union.html)：

* 所有查詢都必須傳回相同數目的欄
* 對應的欄必須具有相同的資料型別

執行時 `UNION` 或 `UNION ALL` 陳述式中，最終輸出中的資料行名稱會反映第一個查詢中的資料行命名。

通常，合併您的 [!DNL Facebook] 和 [!DNL Google AdWords] 將資料花費到 `Data Warehouse View` 需要建立包含七欄的表格，其查詢類似於以下內容：

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

關於上述的幾個要點：

* 為了清楚起見，所有欄都使用上面的別名，以便名稱在所有查詢中相符。 但這並非必要條件。 在SELECT查詢中呼叫欄的順序指示了它們的排列方式。
* 名為的新欄 `ad_source` 是為了更易於篩選而建立的 [!DNL AdWords] 或 [!DNL Facebook] 資料。 請記住，此查詢會結合來自兩個表格的所有資料。 如果您不建立欄，例如 `ad_source`，要識別來自特定來源的支出並不容易。

將以上查詢儲存為 `Data Warehouse View` 建立同時包含兩者的表格 [!DNL Facebook] 和 [!DNL AdWords] 支出，如下所示：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

與其為每個廣告來源建立個別的行銷量度集，您可以利用上表建立單一量度集來擷取所有廣告。

**需要其他協助嗎？**

寫入SQL和建立 `Data Warehouse Views` 技術支援中未提供。 不過， [服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 在建立檢視方面提供協助。 從使用新資料庫移轉舊版資料庫到建立單一Data Warehouse檢視用於特定分析，支援團隊可以提供協助。

通常，建立新的 `Data Warehouse View` 為了合併2-3個類似結構的表格，需要5小時的服務時間，這相當於大約1,250美元的工作。 不過，以下是一些可能會增加所需預期投資的常見因素：

* 將三個以上的表格合併為單一檢視
* 建立多個Data Warehouse檢視
* 複雜的聯結邏輯或篩選條件
* 兩個或多個資料結構不同的資料表的合併
