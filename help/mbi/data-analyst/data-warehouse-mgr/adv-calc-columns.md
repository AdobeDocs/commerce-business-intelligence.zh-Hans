---
title: 進階計算欄型別
description: 瞭解大多數使用欄案例的基本知識 — 但您可能希望計算欄比Data Warehouse管理員可建立的要複雜一些。
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# 進階計算欄型別

您可能想要建立的許多分析都涉及使用 **新欄** 您想要的 `group by` 或 `filter by`. 此 [建立計算欄](../data-warehouse-mgr/creating-calculated-columns.md) 教學課程涵蓋大部分使用案例的基本知識，但您可能會想要讓計算欄比Data Warehouse管理員可建立的要複雜一些。
{： #top}

這些型別的欄可由Data Warehouse分析師的Adobe團隊建立。 若要定義新的計算欄，請提供下列資訊：

1. 此 **`definition`** （包括輸入、公式或格式設定）
1. 此 **`table`** 要在其上建立欄的位置
1. 任何 **`example data points`** 說明欄應包含的內容

以下是進階計算欄的一些常見範例，使用者經常會發現這些範例很實用：

* [依序訂購（或排名）事件](#compareevents)
* [尋找兩個事件之間的時間](#twoevents)
* [比較循序事件值](#sequence)
* [轉換貨幣](#currency)
* [轉換時區](#timezone)
* [其他內容](#else)

## 我正在嘗試依序排序事件 {#compareevents}

這稱為 **事件編號** 計算欄。 這表示您正嘗試尋找特定事件擁有者（例如客戶或使用者）發生事件的順序。

範例如下：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

事件編號計算欄可用來觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

想要檢視實際運作中的客戶訂單編號欄位嗎？ 按一下影像，可檢視在報表中做為分組依據維度使用。

![使用事件編號計算欄至「依客戶訂單編號分組」。](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

若要建立此型別的計算欄，您需要知道：

* 您要建立此欄的表格
* 識別事件擁有者的欄位(`owner\_id` 在此範例中)
* 您要排序事件的欄位(`timestamp` 在此範例中)

[返回頁首](#top)

## 我正在嘗試尋找兩個事件之間的時間。 {#twoevents}

這稱為 `date difference` 計算欄。 這表示您正嘗試根據事件時間戳記，尋找屬於單一記錄之兩個事件之間的時間。

範例如下：

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

日期差異計算欄可用來建立量度，以計算兩個事件之間的平均或中間時間。 按一下以下影像，檢視 `Average time to first order` 量度用於報表中。

![使用日期差異計算欄來計算平均第一筆訂購時間。](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

若要建立此型別的計算欄，您需要知道：

* 您要建立此欄的表格
* 您想知道兩者之間差異的兩個時間戳記

[返回頁首](#top)

## 我正在嘗試比較循序事件值。 {#sequence}

這稱為 **循序事件比較**. 這表示您正嘗試尋找某個值（貨幣、數字、時間戳記）與擁有者上一個事件的對應值之間的差值。

範例如下：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

循序事件比較可用來找出每個循序事件之間的平均或中間時間。 按一下下方影像以檢視 **訂單之間的平均和中位時間** 量度運作中。

=![使用循序事件比較計算欄來計算訂單之間的平均和中位時間。](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

若要建立此型別的計算欄，您需要知道：

* 您要建立此欄的表格
* 識別事件擁有者的欄位(`owner\_id` 在此範例中)
* 您想要檢視每個循序事件(`timestamp` 在此範例中)

[返回頁首](#top)

## 我正在嘗試轉換貨幣。 {#currency}

A **貨幣轉換** 「計算」欄會根據事件時的匯率，將交易金額從記錄的幣別轉換為報表幣別。

範例如下：

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style="table-layout:auto"}

若要建立此型別的計算欄，您需要知道：

* 您要建立此欄的表格
* 您要轉換的交易金額欄
* 指出記錄資料時所用的貨幣（通常是ISO代碼）的欄
* 偏好的報表貨幣

[返回頁首](#top)

## 我正在嘗試轉換時區。 {#timezone}

A **時區轉換** 計算欄會將特定資料來源的時間戳記從記錄的時區轉換為報表時區。

範例如下：

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

若要建立此型別的計算欄，您需要知道：

* 您要建立此欄的表格
* 您要轉換的時間戳記欄
* 記錄資料的時區
* 偏好的報告時區

[返回頁首](#top)

## 我正在嘗試做這裡未列出的事情。 {#else}

不用擔心。 並未列於此處並不表示不可能。 Data Warehouse分析師的Adobe團隊可提供協助。

若要定義新的計算欄， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 提供您想要建置的確切內容的詳細資訊。

## 相關檔案

* [建立計算欄](../data-warehouse-mgr/creating-calculated-columns.md)
* [計算欄型別](../data-warehouse-mgr/calc-column-types.md)
* [建置 [!DNL Google ECommerce] 包含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
