---
title: 使用映射表标准化数据
description: 了解如何使用映射表。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 使用映射表标准化数据

想象一下：你在 `Report Builder`，构建 `Revenue by State` 报表。 你在区里。 一切都在顺畅地前进，直到你加入 `billing state` 分组到您的报表，您会看到以下信息：

![](../../assets/Messy_State_Segments.png)

## 这怎么可能？

遗憾的是，缺乏标准化有时会在构建报表时导致数据混乱和麻烦。 在我们的示例中，我们的客户可能没有下拉菜单或标准化方式来输入其账单状态信息。 这会产生多种值 —  `pa`, `PA`, `penna`, `pennsylvania`和 `Pennsylvania`  — 全部为同一状态，这肯定会导致 `Report Builder`.

可能有一种技术资源可以帮助您清理数据或直接将所需列插入数据库，但如果没有，我们还有另一种解决方案： **映射表**. 通过映射表，您可以通过将数据映射到单个输出，快速轻松地清除和标准化任何混乱的数据。

>[!NOTE]
>
>如果没有我们的支持团队的帮助，就无法为统一表创建映射表。 请联系我们以了解更多信息。

## 如何创建它？ {#how}

**数据格式刷新器：**

* 确保电子表格有一个标题行。
* 避免使用逗号！ 上载文件时会出现问题。
* 使用标准日期格式 `(YYYY-MM-DD HH:MM:SS)` 日期。
* 百分比必须以小数形式输入。
* 确保正确保留任何前导或尾随的零。

在您深入之前，我们建议您 [导出原始表数据](../../tutorials/export-raw-data.md). 首先查看原始数据意味着您可以探索需要清理的数据的所有可能组合，从而确保映射表涵盖所有内容。

要生成映射表，您需要创建一个两列电子表格，其后跟 [文件上载的格式规则](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

在第一列中，输入数据库中存储的值 **每行只有一个值**. 例如， `pa` 和 `PA` 不能位于同一行上 — 每个输入都需要有自己的行。 有关示例，请参阅下文。

在第二列中，输入这些值 **应该**. 如果需要，请继续查看我们的账单状态示例 `pa`, `PA`, `Pennsylvania`和 `pennsylvania` 简直就是 `PA`，我们将输入 `PA` 在此列中输入每个输入值。

![](../../assets/Mapping_table_examples.jpg)

## 在中我需要做什么 [!DNL MBI] 用它？ {#use}

创建完映射表后，您将需要 [上传文件](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] 和 [创建联接列](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 将新字段重新定位到所需表中时，不会将新字段重新定位到该字段。 在文件同步到您的data warehouse后，您可以执行此操作。

在本例中，我们将移动在 `mapping_state` 表(`state_input`) `customer_address` 表。 这样，我们就可以按 `state_input` 列，而不是 `state` 列。

创建 `joined` 列中，导航到在Data warehouse管理器中将字段重新定位到的表。 在本例中，这将是 `customer_address` 表。

1. 单击 **[!UICONTROL Create a Column]**.
1. 选择 `Joined Column` 从 `Definition` 下拉列表。
1. 为列指定一个名称，以将其与 `state` 列。 我们将一起 `billing state (mapped)` 这样，在报表生成器中进行分段时，我们便可以知道要使用哪个列。
1. 我们连接表所需的路径不存在，因此我们需要创建一个新路径。 单击 **[!UICONTROL Create new path]**  在 `Select a table and column` 下拉列表。

   如果不确定表关系是什么或如何正确定义主键和外键，请检出 [我们的教程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 来帮忙。

   * 在 `Many` 侧面，选择要将字段重定位到的表(同样，对于我们，它也是 `customer_address`)和 `Foreign Key` 列，或 `state` 列中。
   * 在 `One` 侧，选择 `mapping` 表格和 `Primary key` 列。 在这种情况下，我们将选择 `state_input` 列 `mapping_state` 表。
   * 以下是路径的外观：

      ![](../../assets/State_Mapping_Path.png)

1. 完成后，单击 **[!UICONTROL Save]** 创建路径。
1. 保存后，路径可能不会立即填充 — 如果发生这种情况，请单击 `Path` 框中，选择您刚刚创建的路径。
1. 单击 **[!UICONTROL Save]** 创建列。

就这样！

## 我现在该怎么做？ {#wrapup}

更新周期完成后，您将能够使用新的联接列对数据进行适当分段，而不是从数据库中对混乱的列进行分段。 看看我们现在的分组选择吧 — 不再有压力混乱：

![](../../assets/Clean_State_Segments.png)

在您想要清理data warehouse中某些可能混乱的数据的任何时候，映射表都会很方便。 但是，映射表也可用于其他一些很酷的用例，如 [在MBI中复制Google Analytics渠道](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 相关

* [了解和评估表关系](../data-warehouse-mgr/table-relationships.md)
* [为计算列创建/删除路径](../data-warehouse-mgr/create-paths-calc-columns.md)
