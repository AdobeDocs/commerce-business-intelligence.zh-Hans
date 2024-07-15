---
title: 使用映射表标准化数据
description: 了解如何使用映射表。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 使用映射表标准化数据

假设您正在`Report Builder`构建`Revenue by State`报表。 在您尝试将`billing state`分组添加到您的报告并且看到以下内容之前，一切进展顺利：

![](../../assets/Messy_State_Segments.png)

## 怎么会这样？

遗憾的是，缺乏标准化有时会导致数据混乱，并在构建报告时带来麻烦。 在此示例中，可能没有下拉菜单或标准化方式可供您的客户输入其计费状态信息。 这会导致不同的值 — `pa`、`PA`、`penna`、`pennsylvania`和`Pennsylvania` — 都处于同一状态，这会导致`Report Builder`中出现一些奇怪的结果。

可能存在一个技术资源，可帮助您清理数据或将所需的列直接插入数据库。 如果没有，则存在其他解决方案 — **映射表**。 映射表允许您将数据映射到单个输出，从而快速、轻松地清除和标准化任何乱数据。

>[!NOTE]
>
>如果没有Adobe支持团队的帮助，则无法为统一表创建映射表。

## 如何创建它？ {#how}

**数据格式刷新程序：**

* 确保您的电子表格具有标题行。
* 避免使用逗号！ 在上传文件时会导致问题。
* 对日期使用标准日期格式`(YYYY-MM-DD HH:MM:SS)`。
* 百分比必须以小数形式输入。
* 请确保正确保留任何前导零或尾随零。

在深入之前，Adobe建议您[导出原始表数据](../../tutorials/export-raw-data.md)。 首先查看原始数据意味着您可以浏览要清理的数据的所有可能组合，从而确保映射表涵盖所有内容。

要生成映射表，您需要创建一个两列电子表格，该电子表格应遵循用于文件上载的[格式化规则](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)。

在第一列中，输入存储在数据库中的值，每行&#x200B;**中仅有一个值**。 例如，`pa`和`PA`不能位于同一行 — 每个输入都需要有自己的行。 有关示例，请参阅下文。

在第二列中，输入这些值&#x200B;**应为**&#x200B;的值。 继续使用计费状态示例，如果您希望`pa`、`PA`、`Pennsylvania`和`pennsylvania`只是`PA`，则应当在此列中为每个输入值输入`PA`。

![](../../assets/Mapping_table_examples.jpg)

## 我需要在[!DNL Commerce Intelligence]中执行什么操作才能使用它？ {#use}

创建完映射表后，必须[将文件](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)上载到[!DNL Commerce Intelligence]和[创建一个联接列](../../data-analyst/data-warehouse-mgr/calc-column-types.md)，该列将新字段重新定位到所需的表中。 将文件同步到Data Warehouse后，即可执行该操作。

此示例使用联接列将您在`mapping_state`表(`state_input`)上创建的列移至`customer_address`表。 这允许我们在报表中按干净的`state_input`列而不是`state`列进行分组。

要创建`joined`列，请在Data Warehouse管理器中导航到字段将重新定位到的表。 在此示例中，这将是`customer_address`表。

1. 单击&#x200B;**[!UICONTROL Create a Column]**。
1. 从`Definition`下拉列表中选择`Joined Column`。
1. 为该列提供一个名称，使其与数据库中的`state`列不同。 为列`billing state (mapped)`命名，以便您能够在Report Builder中进行分段时了解要使用哪个列。
1. 连接表所需的路径不存在，因此您需要创建一个路径。 在`Select a table and column`下拉菜单中单击&#x200B;**[!UICONTROL Create new path]**。

   如果您不确定表关系是什么，或者不确定如何正确定义主键和外键，请查看[教程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)以获取帮助。

   * 在`Many`端，选择您要将该字段重新定位到的表（同样，对我们来说，它是`customer_address`）以及示例中的`Foreign Key`列或`state`列。
   * 在`One`侧，选择`mapping`表和`Primary key`列。 在这种情况下，应从`mapping_state`表中选择`state_input`列。
   * 以下是路径的外观：

     ![](../../assets/State_Mapping_Path.png)

1. 完成后，单击&#x200B;**[!UICONTROL Save]**&#x200B;以创建路径。
1. 路径在保存后可能不会立即填充 — 如果发生这种情况，请单击`Path`框并选择您创建的路径。
1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;以创建列。

## 我现在该怎么办？ {#wrapup}

更新周期完成后，您将能够使用新的联接列正确划分数据，而不是使用数据库中乱七八糟的列。 现在来看看你的分组选项 — 不再有压力混乱：

![](../../assets/Clean_State_Segments.png)

无论您何时想要清理Data Warehouse中一些潜在的乱数据，都可以使用映射表。 但是，映射表也可以用于其他酷炫用例，如[在 [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md)中复制 [!DNL Google Analytics channels] 。

### 相关

* [了解和评估表关系](../data-warehouse-mgr/table-relationships.md)
* [为计算列创建/删除路径](../data-warehouse-mgr/create-paths-calc-columns.md)
