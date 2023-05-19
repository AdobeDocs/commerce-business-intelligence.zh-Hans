---
title: 設定復寫方法
description: 瞭解表格的組織方式，以及表格資料的行為方式，讓您能夠為表格選擇最佳的複製方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# 設定復寫方法

`Replication` 方法和 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md) 用於識別資料庫表格中的新資料或更新資料。 正確設定這些變數對於確保資料正確性和最佳化更新時間至關重要。 本主題著重於復寫方法。

新表格同步於 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)，則會自動為表格選擇復寫方法。 瞭解各種複製方法、表格的組織方式以及表格資料的行為方式，讓您為表格選擇最佳的複製方法。

## 什麼是復寫方法？

`Replication` 方法分為三個群組 —  `Incremental`， `Full Table`、和 `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) 表示 [!DNL Commerce Intelligence] 僅會復寫每次復寫嘗試的新資料或更新資料。 由於這些方法可大幅減少延遲，Adobe建議儘可能使用它。

[**[!UICONTROL Full Table Replication]**](#fulltable) 表示 [!DNL Commerce Intelligence] 會在每次複製嘗試時複製表格的全部內容。 由於要複製的資料量可能很大，這些方法可能會增加延遲和更新時間。 如果表格包含任何時間戳記或日期時間欄，Adobe建議改用增量方法。

**[!UICONTROL Paused]** 表示資料表的復寫已停止或暫停。 [!DNL Commerce Intelligence] 不會在更新週期期間檢查新資料或更新後的資料；這表示不會從以此為複製方法的表格中複製任何資料。

## 增量複製方法 {#incremental}

### 修改時間（最理想）

此 `Modified At` 複製方法使用datetime欄（在建立列時填入，然後在資料變更時更新）來尋找要複製的資料。 此方法的設計是要處理符合下列條件的表格：

* 包含 `datetime` 欄，此欄最初是在建立列時填入，並會在修改列時更新；
* 此 `datetime` 資料行從不為null；
* 不會從表格中刪除列

除了這些條件外，Adobe還建議 **索引** 此 `datetime` 欄用於 `Modified At` 復寫，因為這有助於最佳化復寫速度。

當更新執行時，透過搜尋在下列專案中有值的列來識別新資料或已變更的資料： `datetime` 最近一次更新後發生的欄。 探索到新資料列時，會將它們復寫到您的Data Warehouse。 如果有任何列存在於 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)，則會以目前的資料庫值覆寫。

例如，表格中可能有一欄稱為 `modified\_at` 表示上次變更資料的時間。 如果最新的更新在星期二中午執行，則更新會搜尋所有具有 `modified\_at` 值大於星期二中午。 自星期二中午以來建立或修改的任何探索到的列都會複製到Data Warehouse。

**您知道嗎？**
即使您的資料庫目前無法支援 `Incremental` 複製方法，您也許能夠 [變更您的資料庫](../../best-practices/mod-db-inc-replication.md) 可讓您使用 `Modified At` 或 `Single Auto Incrementing PK`.

`Modified At` 不僅是最理想的複製方法，也是最快速的複製方法。 此方法不僅會在大型資料集時產生顯著的速度提升，而且不需要設定重新檢查選項。 其他方法需要逐一檢視整個表格以識別變更，即使一小部分資料已變更。 `Modified At` 只會反複處理這個小子集。

### 單一自動遞增主索引鍵

`Auto Incrementing` 是循序將主索引鍵指派給資料列的行為。 如果表格為 `Auto Incrementing` 而表格中的最高主索引鍵是1,000，則下一個主值是1,001或更高。 不使用的表格 `Auto Incrementing` 行為可能會將小於1,000的主索引鍵值或跳至大得多的數字，但這不常使用。

此方法旨在從符合下列條件的表格複製新資料：

* `single-column primary key`；和
* `primary key` 資料型別是 `integer`；和
* `auto incrementing` 主索引鍵值。

當表格使用 `Single Auto Incrementing Primary Key` 復寫，透過搜尋高於Data Warehouse中目前最高值的主索引鍵值來探索新資料。 例如，如果Data Warehouse中的最高主鍵值為500，則下次更新執行時，將會搜尋主鍵值為501或更高的列。

### 新增日期

此 `Add Date` 方法的功能類似於 `Single Auto Incrementing Primary Key` 方法。 此方法不會使用整數以作為表格的主索引鍵，而是會使用 `timestamped` 欄以檢查新列。

當表格使用 `Add Date` 復寫，透過搜尋時間戳記值(大於同步至您的Data Warehouse的最新日期)來探索新資料。 例如，如果更新上次執行時間為20/12/2015 09:00:00，則時間戳記大於此值的任何列都會標示為新資料並複製。

>[!NOTE]
>
>不喜歡 `Modified At` 方法， `Add Date` 不會檢查現有列以取得更新資訊 — 它只會期待新列。

## 完整資料表複製方法 {#fulltable}

### 完整表格

`Full table` 復寫會在偵測到新資料列時重新整理整個表格。 這顯然是最不有效的複製方法，因為所有資料都必須在每次更新期間重新處理（假設有新列）。

在同步化程式開始時查詢資料庫並計算列數，即可偵測到新列。 如果您的本機資料庫包含的資料列超過 [!DNL Commerce Intelligence]，則會重新整理表格。 如果列計數相同，或 [!DNL Commerce Intelligence] 包含 *更多* 資料列，則會略過表格。

這引出了以下重要問題 **`Full Table`當發生下列情況時，復寫不相容：**

* 在後續更新週期之間，刪除的資料列多於在本機資料庫表格中建立的資料列，或者
* 欄值已變更，但未建立其他列

在上述任一案例中， `Full Table` 復寫不會偵測到任何變更，且您的資料會過時。 由於此複製方法效率低下，且符合上述要求， `Full Table` 僅建議將復寫作為最後手段。

### 主索引鍵批次

當表格使用 `Primary Key Batch` （PK批次），藉由計算主索引鍵值範圍或批次內的列來探索新資料。 雖然您通常認為這會與整數搭配使用，但文字值的排序方式甚至可讓系統定義常數範圍。

例如，假設更新執行並執行索引鍵1到100範圍的列計數。 在此更新中，系統會尋找並記錄37列。 在下次更新中，會在1-100範圍上再次執行列計數，並找到41列。 由於與上次更新相比列數不同，因此系統會更詳細地檢查該範圍（或批次）。

此方法旨在從符合下列條件的表格複製資料：

* 單欄非整數；或
* 複合索引鍵（包含主索引鍵的多個欄） — 請注意，複合主索引鍵中使用的欄不能有null值；或
* 單欄、整數、不自動增加主索引鍵值。

此方法並不理想，因為為了檢查批次和尋找變更而必須執行的處理量太大，所以速度非常慢。 Adobe建議不要使用此方法，除非無法進行必要的修改以支援其他複製方法。 如果必須使用此方法，預計更新時間會增加。

## 設定復寫方法

複製方法是以逐個表格為基礎設定的。 若要設定表格的復寫方法，您需要 [`Admin`](../../administrator/user-management/user-management.md) 許可權供您存取Data Warehouse管理員。

1. 進入「Data Warehouse管理員」後，從 `Synced Tables` 清單以顯示表格的綱要。
1. 目前的復寫方法列在表格名稱下方。 若要變更，請按一下連結。
1. 在顯示的快顯視窗中，按一下任一專案旁的單選按鈕 `Incremental` 或 `Full Table` 復寫，以選取復寫型別。
1. 接下來，按一下 **[!UICONTROL Replication Method]** 下拉式清單以選取方法。 例如， `Paused` 或 `Modified At`.

   >[!NOTE]
   >
   >**有些增量方法會要求您設定`Replication Key`**. [!DNL Commerce Intelligence] 將使用此索引鍵來決定下一個更新週期應從何處開始。
   >
   >例如，如果您想使用 `modified at` 您的方法 `orders` 表格，您需要設定 `date column` 做為復寫金鑰。 複製金鑰可能有數個選項，但您選取 `created at`，或建立訂單的時間。 如果上次更新週期於2015年12月1日停止:10:00，下一個週期將開始使用 `created at` 日期大於此。

1. 完成後，按一下 **[!UICONTROL Save]**.

檢視整個程式：

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 正在結束

為了完成，您已經將這個表格放在一起，比較各種複製方法。 為Data Warehouse中的表格選取方法非常方便。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 更快 | 慢 | 否 | 否 | 否 | 是 |
| `Primary Key Batch Monitoring` | 慢 | 慢 | 是 | 是 | 是 | 是 |
| `Modified At` | 更快 | 更快 | 是 | 是 | 是 | 否 |

{style="table-layout:auto"}

## 相關檔案

* [瞭解資料重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)
* [修改資料庫以支援 ](../../best-practices/mod-db-inc-replication.md)
* [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
