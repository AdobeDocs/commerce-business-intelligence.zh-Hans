---
title: 配置数据检查
description: 了解如何使用可更改的值配置数据列。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 配置数据检查

在数据库表中，可以有具有可更改值的数据列。 例如，在 `orders`)表中可能存在一个名为 `status`. 当订单最初写入数据库时，状态列可能包含值 _待定_. 随后，订单将复制到 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 此 `pending` 值。

但是，顺序状态可以更改 — 它们并不总是位于 `pending` 状态。 最终，它可能变成 `complete` 或 `cancelled`. 为确保Data warehouse同步此更改，需要重新检查列以获取新值。

这与 [复制方法](../data-warehouse-mgr/cfg-replication-methods.md) 我们讨论过了？ 根据所选的复制方法，重新检查的处理会有所不同。 的 `Modified\_At` 复制方法是处理更改值的最佳选择，因为无需配置重新检查。 的 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新检查配置。

使用以下任一方法时，必须标记可更改的列以进行重新检查。 可以通过三种方法来实现此目的：

* 作为更新的一部分运行的审核过程将标记要重新检查的列。

   >[!NOTE]
   >
   >Auditor依赖于取样过程，因此可能不会立即捕获更改的列。

* 您可以自行设置这些参数，方法是选中Data warehouse管理器中列旁边的复选框，然后单击 **[!UICONTROL Set Recheck Frequency]**，并为应检查更改的时间选择适当的时间间隔。
* 成员 [!DNL MBI] data warehouse团队可以手动标记列以在您的Data warehouse中重新签入。 如果您知道可更改的列，请联系团队以请求设置重新检查。 包括列列表和频度，以及您的请求。

## 重新检查频率 {#frequency}

**你知道吗？**
在 `primary key` 列不会检查列是否有更改的值。 将检查表中是否有已删除的行，然后从Data warehouse中清除所有已删除的行。

标记列以进行重新检查时，您还可以设置重新检查的频率。 如果特定列的更改频率较低，则选择较不频繁的重新检查可以 [优化更新周期](../../best-practices/reduce-update-cycle-time.md).

频率选项包括：

* `always`  — 在每次更新期间进行重新检查
* `daily`  — 对您声明的时区进行午夜后首次更新后，将重新检查
* `weekly`  — 对于您声明的时区，每周在周五晚9点后进行重新检查
* `monthly`  — 对于您声明的时区，周五晚9点后每4周进行一次更新，以便进行重新检查
* `once`  — 仅在下次更新（一次性刷新）中发生

由于更新时间与需要同步的数据量相关，因此我们建议选择 `daily`, `weekly`或 `monthly` 重新检查，而不是每次更新。

## 管理重新检查频率 {#manage}

通过单击表名，然后检查各个列，可以在Data warehouse中管理重新检查频率。 正在同步状态和重新检查频率( **改变？** 列)。

要更改重新选中频率，请单击要更改的列旁边的复选框，然后单击 **[!UICONTROL Set Recheck Frequency]** 下拉列表，然后设置所需的频率。

![](../../assets/dwm-recheck.png)

您有时可能会看到 `Paused` 在 `Changes?` 列。 此值将在表的 [复制方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 设置为 `Paused`.

我们建议您查看这些列，以优化更新并确保重新检查可更改的列。 如果考虑到数据更改的频率，列的重新检查频率不必要地高，我们建议减少该频率以优化更新。

如有问题，请联系我们或查询有关当前复制方法或重新检查的信息。

**相关：**

* [缩短更新时间](../../best-practices/reduce-update-cycle-time.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
