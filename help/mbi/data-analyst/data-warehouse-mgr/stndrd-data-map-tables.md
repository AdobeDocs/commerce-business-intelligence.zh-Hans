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

假设您正在 `Report Builder` 构建 `Revenue by State` 报表。 在您嘗試新增「 」之前，一切順利 `billing state` 分組至您的報表，您會看到以下畫面：

![](../../assets/Messy_State_Segments.png)

## 這怎麼會發生？

遺憾的是，缺乏標準化有時會導致資料混亂，並在建立報告時造成麻煩。 在此範例中，您的客戶可能沒有下拉式選單或標準化方式可輸入其計費狀態資訊。 這會導致各種值 —  `pa`， `PA`， `penna`， `pennsylvania`、和 `Pennsylvania`  — 全部為相同狀態，這會導致中出現一些奇怪的結果 `Report Builder`.

可能有技術資源可協助您清除資料，或直接將所需的欄插入資料庫。 如果沒有，還有另一個解決方案 —  **對應表格**. 對應表格可讓您將資料對應至單一輸出，快速輕鬆地清除任何雜亂的資料並將其標準化。

>[!NOTE]
>
>如果沒有Adobe支援團隊的協助，您就無法建立統一表格的對映表。

## 如何创建它？ {#how}

**数据格式刷新器：**

* 请确保您的电子表格具有标题行。
* 避免使用逗号！ 当您上传文件时，它会导致问题。
* 使用标准日期格式 `(YYYY-MM-DD HH:MM:SS)` 日期。
* 百分比必须以小数位数输入。
* 请确保所有前导或尾随的零都已正确保留。

在进行深入研究之前，Adobe Systems 建议您 [ 导出原始表数据 ](../../tutorials/export-raw-data.md) 。 首先查看原始数据意味着您可以浏览需要清理的数据的所有可能组合，从而确保映射表包含所有内容。

要制作映射表，您需要创建一个双列式电子表格，并遵循 [ 文件上传 ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 的格式规则。

在第一列中，输入存储在数据库 **中每行** 中只有一个值的值。 例如， `pa` 和 `PA` 不能在同一行 — 每個輸入必須有自己的列。 如需範例，請參閱下文。

在第二欄中，輸入這些值 **應為**. 如果您想要的話，繼續使用計費狀態範例 `pa`， `PA`， `Pennsylvania`、和 `pennsylvania` 成為 `PA`，您可以輸入 `PA` 在此欄中為每個輸入值。

![](../../assets/Mapping_table_examples.jpg)

## 我需要做 [!DNL Commerce Intelligence] 些什么才能使用它？ {#use}

创建完映射表后，必须 [ 将该文件 ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 上传到中 [!DNL Commerce Intelligence] ，并 [ 创建一个联接列 ](../../data-analyst/data-warehouse-mgr/calc-column-types.md) ，将新字段重新定位到所需的表中。 您可以在文件同步到数据仓库后执行此操作。

此範例會移動您在 `mapping_state` 表格(`state_input`)重新命名為 `customer_address` 使用聯結欄的表格。 這可讓我們依清理來分組 `state_input` 欄，而非 `state` 欄。

若要建立 `joined` 欄，瀏覽至欄位將在「Data Warehouse管理員」中重新放置到的表格。 在此範例中，這將會是 `customer_address` 表格。

1. 按一下 **[!UICONTROL Create a Column]**.
1. 選取 `Joined Column` 從 `Definition` 下拉式清單。
1. 為欄命名，使其與 `state` 資料行中的資料行。 命名列 `billing state (mapped)` ，以便您可以在报表生成器中划分区段时判断要使用的列。
1. 连接表所需的路径不存在，因此您需要创建一个。 在下拉菜单中 `Select a table and column` 单击 **[!UICONTROL Create new path]** 。

   如果您不确定表关系是什么，或者如何正确定义主键和外键，请查看 [ 教程 ](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 以了解一些帮助。

   * `Many`在侧面，选择要将字段重新定位到的表格（同样，对于我们 `customer_address` 而言）以及 `Foreign Key` 列或 `state` 列（在示例中）。
   * `One`在侧面，选择 `mapping` 表格和 `Primary key` 列。在这种情况下，您可以从 `mapping_state` 表中选择 `state_input` 列。
   * 以下是查看点赞路径的外观：

      ![](../../assets/State_Mapping_Path.png)

1. 完成后，单击 **[!UICONTROL Save]** 以创建路径。
1. 保存后路径可能不会立即填充-如果发生这种情况，请单击 `Path` 该框并选择您创建的路径。
1. 单击 **[!UICONTROL Save]** 以创建列。

## 我现在该怎么做？ {#wrapup}

更新週期完成後，您將能夠使用新的聯結欄來正確地劃分您的資料，而不是從資料庫中劃分混亂的欄。 立即檢視您的分組選項 — 不再有壓力混亂：

![](../../assets/Clean_State_Segments.png)

当您想要清理数据仓库中的某些可能杂乱的数据时，映射表非常有用。 但是，映射表也可用于其他一些酷用例，点赞 [ 复制您  [!DNL Google Analytics channels]  的  [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md) 。

### 相关

* [了解和评估表关系](../data-warehouse-mgr/table-relationships.md)
* [创建/删除计算列的路径](../data-warehouse-mgr/create-paths-calc-columns.md)
