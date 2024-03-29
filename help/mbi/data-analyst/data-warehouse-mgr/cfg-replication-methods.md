---
title: 配置复制方法
description: 了解表如何组织，以及表数据的行为如何允许您为表选择最佳的复制方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# 配置复制方法

`Replication` 方法和 [重新检查](../data-warehouse-mgr/cfg-data-rechecks.md) 用于标识数据库表中的新数据或更新数据。 正确设置这些变量对于确保数据准确性和优化的更新时间至关重要。 本主题侧重于复制方法。

当新表在中同步时 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md)，将自动为表选择复制方法。 通过了解各种复制方法、表的组织方式以及表数据的行为方式，可以为表选择最佳的复制方法。

## 复制方法有哪些？

`Replication` 方法分为三组 —  `Incremental`， `Full Table`、和 `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) 表示 [!DNL Commerce Intelligence] 在每次复制尝试时只复制新的或更新数据。 由于这些方法可显着减少延迟，因此Adobe建议尽可能使用它。

[**[!UICONTROL Full Table Replication]**](#fulltable) 表示 [!DNL Commerce Intelligence] 在每次复制尝试时复制表的全部内容。 由于要复制的数据量可能很大，因此这些方法可能会增加延迟和更新时间。 如果表包含任何带时间戳的列或日期时间列，Adobe建议改用增量方法。

**[!UICONTROL Paused]** 指示表的复制已停止或暂停。 [!DNL Commerce Intelligence] 在更新周期中不会检查新的或更新数据；这意味着不会从使用此项作为复制方法的表中复制任何数据。

## 增量复制方法 {#incremental}

### 修改于（最理想）

此 `Modified At` 复制方法使用datetime列（在创建行时填充，并在数据更改时更新）来查找要复制的数据。 此方法旨在处理符合以下条件的表：

* 包含 `datetime` 创建行时初始填充的列，并在修改行时更新；
* 该 `datetime` 列从不为null；
* 不会从表中删除行

除了这些标准之外，Adobe还建议 **索引** 该 `datetime` 列用于 `Modified At` 复制，因为这有助于优化复制速度。

运行更新时，通过搜索在下列位置具有值的行，可识别新数据或更改的数据： `datetime` 在最近一次更新后出现的列。 当发现新行时，会将它们复制到您的Data Warehouse。 如果有任何行存在于 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md)中，这些值会被当前数据库值覆盖。

例如，一个表可能有一个名为 `modified\_at` 指示上次更改数据的时间。 如果最新的更新在星期二中午运行，则该更新将搜索所有具有 `modified\_at` 值大于星期二中午。 在星期二中午之后创建或修改的任何发现行都将复制到Data Warehouse。

**你知道吗？**
即使您的数据库当前不能支持 `Incremental` 复制方法，您可以 [对数据库进行更改](../../best-practices/mod-db-inc-replication.md) 这样就可以使用 `Modified At` 或 `Single Auto Incrementing PK`.

`Modified At` 它不仅是最理想的复制方法，也是最快速的复制方法。 此方法不仅会在数据集较大时产生显着的速度提升，而且不需要配置重新检查选项。 其他方法需要遍历整个表以标识更改，即使一小部分数据发生了更改也是如此。 `Modified At` 只遍历该小子集。

### 单个自动递增主键

`Auto Incrementing` 是按顺序将主键分配给行的行为。 如果表为 `Auto Incrementing` 并且表中最大的主键为1,000 ，则下一个主值为1,001或更高。 未使用的表 `Auto Incrementing` 行为可能会指定一个小于1,000的主键值或跳转到更大的数字，但通常不使用此值。

此方法旨在从满足以下条件的表中复制新数据：

* `single-column primary key`；和
* `primary key` 数据类型是 `integer`；和
* `auto incrementing` 主键值。

当表使用 `Single Auto Incrementing Primary Key` 复制，通过搜索高于Data Warehouse中当前最高值的主键值来发现新数据。 例如，如果Data Warehouse中的最高主键值为500，则下次更新运行时，它将搜索主键值为501或更高的行。

### 添加日期

此 `Add Date` 方法的功能类似于 `Single Auto Incrementing Primary Key` 方法。 此方法不使用整数以表示表的主键，而是使用 `timestamped` 列以检查新行。

当表使用 `Add Date` 复制，通过搜索时间戳值大于同步到Data Warehouse的最新日期来发现新数据。 例如，如果更新上次运行于2015/20/12/09:00:00，任何时间戳大于此值的行都将被标记为新数据并进行复制。

>[!NOTE]
>
>不像 `Modified At` 方法， `Add Date` 不检查现有行中是否有更新的信息 — 它只向前查找新行。

## 全表复制方法 {#fulltable}

### 完整表

`Full table` 每当检测到新行时，复制都会刷新整个表。 这显然是最不有效的复制方法，因为所有数据必须在每次更新期间重新处理（假定有新行）。

通过在同步过程开始时查询数据库并计算行数来检测新行。 如果本地数据库包含的行数超过 [!DNL Commerce Intelligence]，然后刷新表。 如果行计数相同，或者 [!DNL Commerce Intelligence] 包含 *更多* 行数超过本地数据库的行数，则会跳过该表。

这就提出了一个重要问题 **`Full Table`在以下情况下，复制不兼容：**

* 在后续更新周期之间，删除的行数多于在本地数据库表中创建的行数，或者
* 列值已更改，但未创建其他行

在上述任一情况下， `Full Table` 复制不会检测到任何更改，并且您的数据会过时。 由于这种复制方法效率低下，并且满足上述要求， `Full Table` 仅建议将复制作为最后手段。

### 主键批次

当表使用 `Primary Key Batch` （PK批次），通过计数主键值的范围或批次中的行来发现新数据。 虽然您通常认为这可以与整数一起使用，但也可以通过允许系统定义常量范围的方式对文本值进行排序。

例如，假设更新运行并对从1到100的键范围执行行计数。 在此更新中，系统会查找并记录37行。 在下一次更新中，再次对1-100范围执行行计数，并找到41行。 由于与上次更新相比的行数存在差异，因此系统会更详细地检查该范围（或批次）。

此方法旨在从满足以下条件的表中复制数据：

* 单列非整数；或
* 组合键（包含主键的多个列） — 请注意，在组合主键中使用的列不能具有null值；或
* 单列、整数、不自动增加主键值。

此方法并不理想，因为检查批次和查找更改时必须执行的处理量太大，所以速度非常慢。 Adobe建议不要使用此方法，除非无法进行必要的修改以支持其他复制方法。 如果必须使用此方法，则预计更新时间会增加。

## 设置复制方法

复制方法是逐表设置的。 要为表设置复制方法，您需要 [`Admin`](../../administrator/user-management/user-management.md) 权限，这样您才能访问Data Warehouse管理器。

1. 进入Data Warehouse管理器后，从 `Synced Tables` 列表以显示表的架构。
1. 当前复制方法列在表名下方。 要更改它，请单击链接。
1. 在显示的弹出窗口中，单击其中任一按钮旁边的单选按钮 `Incremental` 或 `Full Table` 复制，以选择复制类型。
1. 接下来，单击 **[!UICONTROL Replication Method]** 下拉列表以选择方法。 例如， `Paused` 或 `Modified At`.

   >[!NOTE]
   >
   >**有些增量方法需要您设置`Replication Key`**. [!DNL Commerce Intelligence] 将使用此键来确定下一个更新周期应该从何处开始。
   >
   >例如，如果要使用 `modified at` 方法 `orders` 表，您需要设置 `date column` 作为复制密钥。 复制密钥可能有多个选项，但您选择 `created at`，或创建订单的时间。 如果上次更新周期停止于2015年12月1日00:10:00，下一个周期将开始使用 `created at` 日期晚于此。

1. 完成后，单击 **[!UICONTROL Save]**.

看看整个过程：

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

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
* [修改数据库以支持 ](../../best-practices/mod-db-inc-replication.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
* [减少更新时间](../../best-practices/reduce-update-cycle-time.md)
