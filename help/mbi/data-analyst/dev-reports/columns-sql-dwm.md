---
title: SQL与Data warehouse管理器之间的差异
description: 了解SQL与Data warehouse管理器之间的差异。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# SQL与Data warehouse管理器之间的差异

在 [SQLReport Builder](../dev-reports/sql-rpt-bldr.md) 和使用 [data warehouse管理器](../data-warehouse-mgr/creating-calculated-columns.md):一个是对更新周期的依赖，另一个是列在帐户中的保存方式。

## 中的列 `SQL Report Builder`

列不依赖于更新周期，因此您不必再等待一个周期完成，即可对列进行迭代。 如果你犯了错误，只需按几下键来纠正它 — 无需再等待两次更新完成，然后你才能恢复工作。

>[!IMPORTANT]
>
>使用SQL编辑器创建的列不会保存到您的Data warehouse。 您始终有权访问包含列的查询，但如果要在多个报表中使用列，则必须在每个报表的查询中重新创建列。 这意味着使用SQL编辑器创建的列不能在传统 `Report Builder`.

## data warehouse管理器中的列

列取决于更新周期，因此必须先完成整个周期，然后才能进行编辑。 这些列将保存到Data warehouse管理器中，并可在传统 `Report Builder` 或 `SQL Report Builder`.
