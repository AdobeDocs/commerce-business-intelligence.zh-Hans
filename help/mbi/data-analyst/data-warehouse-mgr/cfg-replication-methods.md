---
title: 配置复制方法
description: 了解表的组织方式以及表数据的行为方式将允许您为表选择最佳的复制方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# 配置复制方法

`Replication` 方法和 [重新检查](../data-warehouse-mgr/cfg-data-rechecks.md) 用于标识数据库表中的新数据或更新的数据。 正确设置参数对于确保数据准确性和优化更新时间都至关重要。 在本文中，我们将重点介绍复制方法。

在Data warehouse管理器中同步新表时，将自动为该表选择复制方法。 了解各种复制方法、表的组织方式以及表数据的行为方式将允许您为表选择最佳的复制方法。

## 什么是复制方法？

`Replication` 方法分为三组 —  `Incremental`, `Full Table`和 `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) 意味着 [!DNL MBI] 将仅在每次复制尝试时复制新数据或更新数据。 由于这些方法将显着减少延迟，因此我们强烈建议尽可能使用它。

[**[!UICONTROL Full Table Replication]**](#fulltable) 意味着 [!DNL MBI] 将在每次复制尝试时复制表的整个内容。 由于要复制的数据量可能很大，因此这些方法可能会增加延迟和更新时间。 如果表包含任何带有时间戳的列或日期时间列，我们建议改用增量方法。

**[!UICONTROL Paused]** 表示表的复制已停止或暂停。 [!DNL MBI] 在更新周期中，将不检查新数据或更新数据；这意味着不会从将其作为其复制方法的表中复制任何数据。

## 增量复制方法 {#incremental}

### 修改时间（最理想）

的 `Modified At` 复制方法使用datetime列（创建行时填充，数据更改时更新）来查找要复制的数据。 此方法旨在处理满足以下条件的表：

* 包含a `datetime` 列，在创建行时最初填充该列，并在修改行时更新该列；
* the `datetime` 列从不为空；
* 不会从表中删除行

除了这些标准外，我们还强烈建议 **索引** the `datetime` 用于 `Modified At` 复制，因为这样有助于优化复制速度。

运行更新时，通过搜索 `datetime` 最近一次更新后发生的列。 发现新行后，这些行将被复制到您的Data warehouse。 如果Data warehouse中已存在任何行，则将使用当前数据库值覆盖这些行。

例如，表可能具有一个名为 `modified\_at` 表示上次更改数据的时间。 如果最近的更新在星期二中午运行，则更新将搜索所有具有 `modified\_at` 值大于星期二中午。 自星期二中午以来创建或修改的任何已发现行都将复制到Data warehouse。

**你知道吗？**
即使您的数据库当前不支持 `Incremental` 复制方法，您可以 [对数据库进行一些更改](../../best-practices/mod-db-inc-replication.md) 能够使用 `Modified At` 或 `Single Auto Incrementing PK`.

`Modified At` 不仅是最理想的复制方法，而且速度最快。 此方法不仅会在大型数据集中产生显着的速度增长，而且不需要配置重新检查选项。 其他方法将需要遍历整个表来识别更改，即使一小部分数据发生了更改也是如此。 `Modified At` 只遍历小子集。

### 单个自动递增主键

`Auto Incrementing` 是按顺序将主键分配给行的行为。 如果表为 `Auto Incrementing` 表中最高的主键当前为1000，则下一个主键值将为1001或更高。 不使用的表 `Auto Incrementing` 行为可能会分配一个小于1000的主键值，或跳转到一个大得多的数字，但不常用。

此方法旨在从满足以下条件的表中复制新数据：

* `single-column primary key`;和
* `primary key` 数据类型 `integer`;和
* `auto incrementing` 主键值。

当表使用 `Single Auto Incrementing Primary Key` 复制时，通过搜索主键值，发现新数据，该主键值大于Data warehouse中当前的最高值。 例如，如果Data warehouse中最高的主键值为500，则下次运行更新时，将搜索主键值为501或更高的行。

### 添加日期

的 `Add Date` 方法函数与类似 `Single Auto Incrementing Primary Key` 方法。 此方法将使用 `timestamped` 列来检查新行。

当表使用 `Add Date` 复制时，会通过搜索加盖时间戳的值来发现新数据，这些值大于与您的Data warehouse同步的最新日期。 例如，如果上次运行更新的时间为20/12/2015 09:00:00，时间戳大于此时间戳的任何行都将标记为新数据并进行复制。

>[!NOTE]
>
>与 `Modified At` 方法， `Add Date` 将不检查现有行以了解更新的信息 — 只会期待看到新行。

## 完整表复制方法 {#fulltable}

### 完整表

`Full table` 每次检测到新行时，复制都会刷新整个表。 这是迄今为止最不有效的复制方法，因为假设存在新行，那么每次更新期间都必须重新处理所有数据。

在同步过程开始时，通过查询数据库并计数行数来检测新行。 如果本地数据库包含的行数多于 [!DNL MBI]，则会刷新表。 如果行计数相同，或者 [!DNL MBI] 包含 *更多* 行，则会跳过表。

这就引出了一个重要的问题 **`Full Table`复制在以下情况下不兼容：**

* 在后续更新周期之间删除的行数多于在本地数据库表中创建的行数，或者
* 列值已更改，但未创建其他行

在上述任一情况下， `Full Table` 复制不会检测到任何更改，并且您的数据将失效。 由于此复制方法效率低下，以及上述要求， `Full Table` 仅建议最后采用复制。

### 主键批

当表使用 `Primary Key Batch` （PK批），则新数据通过对主键值范围或批中的行进行计数来发现。 虽然我们通常认为这会与整数一起使用，但即使文本值也可以按允许系统定义常量范围的方式进行排序。

例如，假设更新运行并对1到100之间的键值范围执行行计数。 在此更新中，系统查找并记录37行。 在下次更新中，将再次对1-100范围执行行计数，并找到41行。 由于行数与上次更新有所不同，因此系统将更详细地检查该范围（或批）。

此方法旨在从满足以下条件的表中复制数据：

* 单列非整数；或
* 复合键（包含主键的多列） — 请注意，复合主键中使用的列永远不能具有空值；或
* 单列、整数、非自动递增主键值。

此方法不理想，因为由于必须进行大量处理才能检查批次并查找更改，因此速度极慢。 我们不建议使用此方法，除非无法进行支持其他复制方法所必需的修改。 如果必须使用此方法，则更新时间会增加。

## 设置复制方法

复制方法是逐表设置的。 要为表设置复制方法，您需要 [`Admin`](../../administrator/user-management/user-management.md) 权限，以便您能够访问Data warehouse管理器。

1. 进入Data warehouse管理器后，从 `Synced Tables` 列表以显示表的架构。
1. 当前复制方法列在表名下方。 要更改此链接，请单击。
1. 在显示的弹出窗口中，单击任一 `Incremental` 或 `Full Table` 复制以选择复制类型。
1. 接下来，单击 **[!UICONTROL Replication Method]** 下拉列表以选择方法 — 例如， `Paused` 或 `Modified At`.

   >[!NOTE]
   >
   >**某些增量方法要求您设置`Replication Key`**. [!DNL MBI] 将使用此键来确定下一个更新周期应该开始的位置。
   >
   >例如，如果我们要使用 `modified at` 方法 `orders` 表格，我们需要设置 `date column` 作为复制密钥。 复制键可能存在多个选项，但我们将选择 `created at`，或创建订单的时间。 如果上次更新周期在12/1/2015 00停止:10:00，下一个周期将开始使用 `created at` 日期大于此。

1. 完成后，单击 **[!UICONTROL Save]**.

查看整个过程：

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 包装

最后，我们整理了这个表格，比较了各种复制方法。 我们发现，在为data warehouse中的表选择方法时，它非常方便。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 更快 | 慢 | 否 | 否 | 否 | 是 |
| `Primary Key Batch Monitoring` | 慢 | 慢 | 是 | 是 | 是 | 是 |
| `Modified At` | 更快 | 更快 | 是 | 是 | 是 | 否 |

{style=&quot;table-layout:auto&quot;}

## 相关文档

* [了解数据重新检查](../data-warehouse-mgr/cfg-data-rechecks.md)
* [修改数据库以支持 ](../../best-practices/mod-db-inc-replication.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
* [缩短更新时间](../../best-practices/reduce-update-cycle-time.md)
