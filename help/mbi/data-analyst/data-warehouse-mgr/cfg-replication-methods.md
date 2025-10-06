---
title: 配置复制方法
description: 了解表如何组织，以及表数据的行为如何允许您为表选择最佳的复制方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# 配置复制方法

`Replication`方法和[重新检查](../data-warehouse-mgr/cfg-data-rechecks.md)用于标识数据库表中的新数据或更新数据。 正确设置这些变量对于确保数据准确性和优化的更新时间至关重要。 本主题侧重于复制方法。

在[Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)中同步新表时，将自动为该表选择复制方法。 通过了解各种复制方法、表的组织方式以及表数据的行为方式，可以为表选择最佳的复制方法。

## 复制方法有哪些？

`Replication`方法分为三组 — `Incremental`、`Full Table`和`Paused`。

[**[!UICONTROL Incremental Replication]**](#incremental)意味着[!DNL Commerce Intelligence]在每次复制尝试时只复制新的或更新数据。 由于这些方法可显着减少延迟，因此Adobe建议尽可能使用它。

[**[!UICONTROL Full Table Replication]**](#fulltable)表示[!DNL Commerce Intelligence]在每次复制尝试时复制表的全部内容。 由于要复制的数据量可能很大，因此这些方法可能会增加延迟和更新时间。 如果表包含任何带时间戳的列或日期时间列，Adobe建议改用增量方法。

**[!UICONTROL Paused]**&#x200B;表示表的复制已停止或暂停。 [!DNL Commerce Intelligence]不会在更新周期中检查新数据或更新数据；这意味着不会从将此作为复制方法的表中复制任何数据。

## 增量复制方法 {#incremental}

### 修改于（最理想）

`Modified At`复制方法使用datetime列（在创建行时填充，并在数据更改时更新）来查找要复制的数据。 此方法旨在处理符合以下条件的表：

* 包含`datetime`列，该列最初是在创建行时填充的，并在修改行时更新；
* `datetime`列从不为null；
* 不会从表中删除行

除了这些条件外，Adobe还建议为用于&#x200B;**复制的**&#x200B;列`datetime`编制索引`Modified At`，因为这有助于优化复制速度。

当更新运行时，通过搜索在最近更新之后发生的`datetime`列中带有值的行来识别新数据或更改的数据。 当发现新行时，会将它们复制到Data Warehouse。 如果[Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)中存在任何行，则当前数据库值将覆盖这些行。

例如，一个表可能有一个名为`modified\_at`的列，它指示上次更改数据的时间。 如果最新更新在星期二中午运行，则该更新将搜索星期二中午具有`modified\_at`值大于星期二的所有行。 在星期二中午之后创建或修改的任何发现行都将复制到Data Warehouse。

**您知道吗？**
即使您的数据库当前不能支持`Incremental`复制方法，您也可以[对您的数据库进行更改](../../best-practices/mod-db-inc-replication.md)，以便能够使用`Modified At`或`Single Auto Incrementing PK`。

`Modified At`不仅是最理想的复制方法，也是最快的复制方法。 此方法不仅会在数据集较大时产生显着的速度提升，而且不需要配置重新检查选项。 其他方法需要遍历整个表以标识更改，即使一小部分数据发生了更改也是如此。 `Modified At`仅迭代该小子集。

### 单个自动递增主键

`Auto Incrementing`是按顺序将主键分配给行的行为。 如果某个表为`Auto Incrementing`，而该表中最高主键为1,000，则下一个主值为1,001或更高。 不使用`Auto Incrementing`行为的表可以分配小于1,000的主键值或跳转到更大的数字，但这不是常用的。

此方法旨在从满足以下条件的表中复制新数据：

* `single-column primary key`；和
* `primary key`数据类型是`integer`；并且
* `auto incrementing`主键值。

当表使用`Single Auto Incrementing Primary Key`复制时，通过搜索高于Data Warehouse中当前最高值的主键值来发现新数据。 例如，如果Data Warehouse中的最高主键值为500，则当下次更新运行时，它将搜索主键值为501或更高的行。

### 添加日期

`Add Date`方法的功能与`Single Auto Incrementing Primary Key`方法类似。 此方法使用`timestamped`列来检查新行，而不是使用整型作为表的主键。

当表使用`Add Date`复制时，通过搜索时间戳值来发现新数据，这些值大于同步到Data Warehouse的最新日期。 例如，如果更新上次运行时间为20/12/2015 09:00:00，则时间戳大于该时间戳的任何行都将标记为新数据并进行复制。

>[!NOTE]
>
>与`Modified At`方法不同，`Add Date`不检查现有行中是否有更新的信息 — 它只向前查找新行。

## 全表复制方法 {#fulltable}

### 完整表

在检测到新行时，`Full table`复制会刷新整个表。 这显然是最不有效的复制方法，因为所有数据必须在每次更新期间重新处理（假定有新行）。

通过在同步过程开始时查询数据库并计算行数来检测新行。 如果本地数据库包含的行数超过[!DNL Commerce Intelligence]个，则表会被刷新。 如果行数相同，或者[!DNL Commerce Intelligence]包含的行数比本地数据库多&#x200B;*个*&#x200B;行，则会跳过该表。

这会引出&#x200B;**`Full Table`复制在以下情况下不兼容的重要点：**

* 在后续更新周期之间，删除的行数多于在本地数据库表中创建的行数，或者
* 列值已更改，但未创建其他行

在上述任一情况下，`Full Table`复制不会检测到任何更改，并且您的数据会过时。 由于此复制方法效率低下，并且满足上述要求，因此，最后才建议使用`Full Table`复制。

### 主键批次

当表使用`Primary Key Batch` （PK批次）时，通过计数主键值的范围或批次中的行来发现新数据。 虽然您通常认为这可以与整数一起使用，但也可以通过允许系统定义常量范围的方式对文本值进行排序。

例如，假设更新运行并对从1到100的键范围执行行计数。 在此更新中，系统会查找并记录37行。 在下一次更新中，再次对1-100范围执行行计数，并找到41行。 由于与上次更新相比的行数存在差异，因此系统会更详细地检查该范围（或批次）。

此方法旨在从满足以下条件的表中复制数据：

* 单列非整数；或
* 组合键（包含主键的多个列） — 请注意，在组合主键中使用的列不能具有null值；或
* 单列、整数、不自动增加主键值。

此方法并不理想，因为检查批次和查找更改时必须执行的处理量太大，所以速度非常慢。 Adobe建议不要使用此方法，除非无法进行必要的修改以支持其他复制方法。 如果必须使用此方法，则预计更新时间会增加。

## 设置复制方法

复制方法是逐表设置的。 要为表设置复制方法，您需要[`Admin`](../../administrator/user-management/user-management.md)权限，才能访问Data Warehouse Manager。

1. 进入Data Warehouse Manager后，从`Synced Tables`列表中选择该表以显示该表的架构。
1. 当前复制方法列在表名下方。 要更改它，请单击链接。
1. 在显示的弹出窗口中，单击`Incremental`或`Full Table`复制旁边的单选按钮以选择复制类型。
1. 接下来，单击&#x200B;**[!UICONTROL Replication Method]**&#x200B;下拉菜单以选择方法。 例如，`Paused`或`Modified At`。

   >[!NOTE]
   >
   >**某些增量方法需要您设置`Replication Key`**。 [!DNL Commerce Intelligence]将使用此键来确定下一个更新周期的开始位置。
   >
   >例如，如果要为`modified at`表使用`orders`方法，则需要将`date column`设置为复制密钥。 可能存在多个复制密钥选项，但您选择了`created at`或创建订单的时间。 如果上一个更新周期在12/1/2015 00:10:00停止，则下一个周期将开始复制日期大于此日期的`created at`数据。

1. 完成后，单击&#x200B;**[!UICONTROL Save]**。

看看整个过程：

![为数据库表配置复制方法的动画演示](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 正在结束

最后，您将此表放在一起，比较各种复制方法。 在为Data Warehouse中的表选择方法时，这种方法非常方便。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 更快 | 慢速 | 否 | 否 | 否 | 是 |
| `Primary Key Batch Monitoring` | 慢速 | 慢速 | 是 | 是 | 是 | 是 |
| `Modified At` | 更快 | 更快 | 是 | 是 | 是 | 否 |

{style="table-layout:auto"}

## 相关文档

* [了解数据重新检查](../data-warehouse-mgr/cfg-data-rechecks.md)
* [修改数据库以支持 &#x200B;](../../best-practices/mod-db-inc-replication.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
* [减少更新时间](../../best-practices/reduce-update-cycle-time.md)
