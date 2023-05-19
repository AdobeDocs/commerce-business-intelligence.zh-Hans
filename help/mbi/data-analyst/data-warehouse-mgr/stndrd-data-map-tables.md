---
title: 使用對應表格標準化資料
description: 瞭解如何使用對應表格。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 使用對應表格標準化資料

想像您身在 `Report Builder` 建立 `Revenue by State` 報告。 在您嘗試新增「 」之前，一切順利 `billing state` 分組至您的報表，您會看到以下畫面：

![](../../assets/Messy_State_Segments.png)

## 這怎麼會發生？

遺憾的是，缺乏標準化有時會導致資料混亂，並在建立報告時造成麻煩。 在此範例中，您的客戶可能沒有下拉式選單或標準化方式可輸入其計費狀態資訊。 這會導致各種值 —  `pa`， `PA`， `penna`， `pennsylvania`、和 `Pennsylvania`  — 全部為相同狀態，這會導致中出現一些奇怪的結果 `Report Builder`.

可能有技術資源可協助您清除資料，或直接將所需的欄插入資料庫。 如果沒有，還有另一個解決方案 —  **對應表格**. 對應表格可讓您將資料對應至單一輸出，快速輕鬆地清除任何雜亂的資料並將其標準化。

>[!NOTE]
>
>如果沒有Adobe支援團隊的協助，您就無法建立統一表格的對映表。

## 如何建立？ {#how}

**資料格式重新整理程式：**

* 請確定您的試算表有標題列。
* 避免使用逗號！ 上傳檔案時會造成問題。
* 使用標準日期格式 `(YYYY-MM-DD HH:MM:SS)` 用於日期。
* 百分比必須以小數點輸入。
* 請確定正確保留任何開頭或結尾的零。

潛入之前，Adobe建議您 [匯出原始資料表資料](../../tutorials/export-raw-data.md). 首先檢視原始資料表示您可以探索您需要清理的資料的所有可能組合，從而確保對應表格涵蓋所有內容。

若要建立對映表格，您需要建立一個兩欄式試算表，並遵循 [檔案上傳的格式化規則](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

在第一欄中，輸入儲存在資料庫中的值 **每列只有一個值**. 例如， `pa` 和 `PA` 不能在同一行 — 每個輸入必須有自己的列。 如需範例，請參閱下文。

在第二欄中，輸入這些值 **應為**. 如果您想要的話，繼續使用計費狀態範例 `pa`， `PA`， `Pennsylvania`、和 `pennsylvania` 成為 `PA`，您可以輸入 `PA` 在此欄中為每個輸入值。

![](../../assets/Mapping_table_examples.jpg)

## 我需要做什麼 [!DNL Commerce Intelligence] 以使用它？ {#use}

完成建立對應表格之後，您必須 [上傳檔案](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 到 [!DNL Commerce Intelligence] 和 [建立聯結欄](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 會將新欄位重新定位到所需的表格中。 將檔案同步至您的Data Warehouse後，您就可以執行此動作。

此範例會移動您在 `mapping_state` 表格(`state_input`)重新命名為 `customer_address` 使用聯結欄的表格。 這可讓我們依清理來分組 `state_input` 欄，而非 `state` 欄。

若要建立 `joined` 欄，瀏覽至欄位將在「Data Warehouse管理員」中重新放置到的表格。 在此範例中，這將會是 `customer_address` 表格。

1. 按一下 **[!UICONTROL Create a Column]**.
1. 選取 `Joined Column` 從 `Definition` 下拉式清單。
1. 為欄命名，使其與 `state` 資料行中的資料行。 為欄命名 `billing state (mapped)` 以便您分辨在report builder中分段時要使用的欄。
1. 您需要連線表格的路徑不存在，因此您需要建立一個路徑。 按一下 **[!UICONTROL Create new path]**  在 `Select a table and column` 下拉式清單。

   如果您不確定表格關係是什麼，或不確定如何正確定義主索引鍵和外索引鍵，請出庫 [教學課程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 以取得協助。

   * 於 `Many` 在側，選取您要重新放置欄位的表格(同樣地，對我們來說，它是 `customer_address`)和 `Foreign Key` 欄，或 `state` 欄，在範例中。
   * 於 `One` 側，選取 `mapping` 表格和 `Primary key` 欄。 在此情況下，您可以選取 `state_input` 欄來自 `mapping_state` 表格。
   * 以下是該路徑的外觀：

      ![](../../assets/State_Mapping_Path.png)

1. 完成後，按一下 **[!UICONTROL Save]** 以建立路徑。
1. 路徑在儲存後可能不會立即填入 — 如果發生這種情況，請按一下 `Path` 方塊並選取您建立的路徑。
1. 按一下 **[!UICONTROL Save]** 以建立欄。

## 我現在該做什麼？ {#wrapup}

更新週期完成後，您將能夠使用新的聯結欄來正確地劃分您的資料，而不是從資料庫中劃分混亂的欄。 立即檢視您的分組選項 — 不再有壓力混亂：

![](../../assets/Clean_State_Segments.png)

無論您何時想要清除Data Warehouse中某些可能雜亂的資料，對應表格都相當方便。 不過，對應表格也可用於其他酷炫的使用案例，例如 [複製您的 [!DNL Google Analytics channels] 在 [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 相關

* [瞭解和評估表格關係](../data-warehouse-mgr/table-relationships.md)
* [建立/刪除計算欄的路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
