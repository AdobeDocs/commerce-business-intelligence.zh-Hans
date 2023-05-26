---
title: 使用映射表标准化数据
description: 了解如何使用映射表。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 使用映射表标准化数据

想象你在 `Report Builder` 构建 `Revenue by State` 报告。 在您尝试添加 `billing state` 分组到您的报表，您会看到以下内容：

![](../../assets/Messy_State_Segments.png)

## 这怎么会发生？

遗憾的是，缺乏标准化有时会导致数据混乱，并在构建报告时带来麻烦。 在本例中，您的客户可能没有下拉菜单或标准化方式来输入其计费状态信息。 这会导致出现各种值 —  `pa`， `PA`， `penna`， `pennsylvania`、和 `Pennsylvania`  — 全部为同一状态，这会导致在 `Report Builder`.

可能存在一个技术资源，可帮助您清理数据或将所需的列直接插入数据库。 如果答案是否定的，还有另一种解决方案： **映射表**. 映射表允许您将数据映射到单个输出，从而快速、轻松地清除和标准化任何混乱的数据。

>[!NOTE]
>
>如果没有Adobe支持团队的帮助，则无法为统一表创建映射表。

## 如何创建它？ {#how}

**数据格式刷新程序：**

* 确保您的电子表格具有标题行。
* 避免使用逗号！ 上传文件时会导致问题。
* 使用标准日期格式 `(YYYY-MM-DD HH:MM:SS)` 用于日期。
* 百分比必须以小数形式输入。
* 确保正确保留任何前导零或尾随零。

在深入之前，Adobe建议您 [导出原始表数据](../../tutorials/export-raw-data.md). 首先查看原始数据意味着您可以探索需要清理的数据的所有可能组合，从而确保映射表涵盖所有内容。

要生成映射表，您需要创建一个两列电子表格，该表格应遵循 [格式化文件上传的规则](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

在第一列中，输入存储在数据库中的值 **每行只有一个值**. 例如， `pa` 和 `PA` 不能位于同一行 — 每个输入都需要有自己的行。 有关示例，请参阅下文。

在第二列中，输入以下值 **应为**. 继续使用计费状态示例（如果需要） `pa`， `PA`， `Pennsylvania`、和 `pennsylvania` 简单地 `PA`，您可以输入 `PA` 在此列中为每个输入值。

![](../../assets/Mapping_table_examples.jpg)

## 我需要做什么 [!DNL Commerce Intelligence] 使用它？ {#use}

创建完映射表后，必须 [上传文件](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 到 [!DNL Commerce Intelligence] 和 [创建联接列](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 该选项会将新字段重新定位到所需的表中。 将文件同步到Data warehouse后，即可执行此操作。

此示例移动您在 `mapping_state` 表(`state_input`)到 `customer_address` 使用联接列的表。 这允许我们按清理进行分组 `state_input` 列而不是 `state` 列。

要创建 `joined` 列中，导航到字段将在Data warehouse管理器中重新定位到的表。 在本例中，这将 `customer_address` 表格。

1. 单击 **[!UICONTROL Create a Column]**.
1. 选择 `Joined Column` 从 `Definition` 下拉菜单。
1. 为列提供一个名称，使其与 `state` 列中的值。 为列命名 `billing state (mapped)` 这样您就可以在Report Builder中进行分段时知道要使用哪一列。
1. 连接表所需的路径不存在，因此您需要创建一个路径。 单击 **[!UICONTROL Create new path]**  在 `Select a table and column` 下拉菜单。

   如果您不确定表关系是什么，或者不确定如何正确定义主键和外键，请查看 [教程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 以寻求帮助。

   * 在 `Many` 侧，选择要将该字段重新定位到的表(同样，对于我们来说，它是 `customer_address`)和 `Foreign Key` 列，或 `state` 列，在本例中。
   * 在 `One` 侧，选择 `mapping` 表格和 `Primary key` 列。 在这种情况下，您可以选择 `state_input` 中的列 `mapping_state` 表格。
   * 下面是路径的外观：

      ![](../../assets/State_Mapping_Path.png)

1. 完成后，单击 **[!UICONTROL Save]** 以创建路径。
1. 路径在保存后可能不会立即填充 — 如果发生这种情况，请单击 `Path` 框并选择您创建的路径。
1. 单击 **[!UICONTROL Save]** 以创建列。

## 我现在该做什么？ {#wrapup}

更新周期完成后，您将能够使用新联接的列来正确划分数据，而不是从数据库中划分混乱的列。 立即查看您的分组选项 — 不再有压力混乱：

![](../../assets/Clean_State_Segments.png)

无论您何时想要清理Data warehouse中一些潜在的混乱数据，映射表都非常方便。 但是，映射表也可以用于其他一些很酷的用例，例如 [复制您的 [!DNL Google Analytics channels] 在 [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 相关

* [了解和评估表关系](../data-warehouse-mgr/table-relationships.md)
* [为计算列创建/删除路径](../data-warehouse-mgr/create-paths-calc-columns.md)
