---
title: 配置数据检查
description: 了解如何使用可变值配置数据列。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 配置数据检查

在数据库表中，可以存在具有可变值的数据列。 例如，在 `orders`)表可能有一个名为的列 `status`. 最初将订单写入数据库时， status列可能包含值 _待处理_. 订单会复制到您的 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 使用此 `pending` 值。

但是，订单状态可以更改 — 它们并不总是处于 `pending` 状态。 最终，它可能会变成 `complete` 或 `cancelled`. 要确保Data warehouse同步此更改，必须重新检查列以查找新值。

这与 [复制方法](../data-warehouse-mgr/cfg-replication-methods.md) 已经讨论过了？ 重新检查的处理方式因选择的复制方法而异。 此 `Modified\_At` 复制方法是处理更改值的最佳选择，因为不必配置重新检查。 此 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新检查配置。

使用这两种方法之一时，必须标记可更改列以重新检查。 有三种方法可以做到这一点：

* 作为要重新检查的更新标志列的一部分运行的审核进程。

   >[!NOTE]
   >
   >审计人员依靠的是抽样过程，更改列可能不会立即捕获。

* 您可以通过选中Data warehouse管理器中列旁边的复选框，然后单击 **[!UICONTROL Set Recheck Frequency]**，并为应检查更改的时间选择适当的时间间隔。
* 成员隶属于 [!DNL MBI] data warehouse团队可以手动标记列，以便在您的Data warehouse中重新签入。 如果您知道可更改列，请与团队联系以请求设置重新检查。 在请求中包含列列表以及频率。

## 重新检查频率 {#frequency}

**你知道吗？**
在上设置重新检查 `primary key` 列不检查列是否有更改的值。 将检查表中是否删除了行，并且所有删除操作都将从Data warehouse中清除。

当列被标记为要重新检查时，您还可以设置重新检查的频率。 如果特定列不经常更改，则选择不太频繁的重新检查可以 [优化更新周期](../../best-practices/reduce-update-cycle-time.md).

频率选项包括：

* `always`  — 在每次更新期间进行重新检查
* `daily`  — 对声明的时区进行首次午夜后更新时进行重新检查
* `weekly`  — 对于您声明的时区，在每周的星期五晚上9点后进行重新检查
* `monthly`  — 对于您声明的时区，在星期五晚上9点后每四周更新一次，此时将重新检查
* `once`  — 仅在下次更新（一次性刷新）时发生

由于更新时间与需要同步的数据量相关，因此Adobe建议选择 `daily`， `weekly`，或 `monthly` 重新检查而不是每次更新。

## 管理重新检查频率 {#manage}

通过单击表名，然后检查各个列，可以在Data warehouse中管理重新检查频率。 同步状态和重新检查频率(即 **更改？** 列)。

要更改重新检查频率，请单击要更改的列旁边的复选框。 然后单击 **[!UICONTROL Set Recheck Frequency]** 下拉菜单并设置所需的频率。

![](../../assets/dwm-recheck.png)

您有时可能会看到 `Paused` 在 `Changes?` 列。 当表的 [复制方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 设置为 `Paused`.

Adobe建议查看这些列以优化更新并确保重新检查可更改的列。 如果给定数据更改的频率，列的重新检查频率很高，Adobe建议降低它以优化更新。

如有疑问，请联系我们，或者查询当前的复制方法或重新检查。

**相关：**

* [缩短更新时间](../../best-practices/reduce-update-cycle-time.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
