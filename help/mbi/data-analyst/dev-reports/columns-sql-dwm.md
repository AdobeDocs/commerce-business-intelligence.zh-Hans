---
title: SQL和Data warehouse管理器之间的区别
description: 了解SQL和Data warehouse管理器之间的区别。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# SQL和Data warehouse管理器之间的区别

在中创建的列之间存在两个主要区别 [SQLREPORT BUILDER](../dev-reports/sql-rpt-bldr.md) 以及使用 [data warehouse管理器](../data-warehouse-mgr/creating-calculated-columns.md). 一个是与更新周期的依赖关系，另一个是列在帐户中的保存方式。

## 中的列 `SQL Report Builder`

列不依赖于更新周期，因此无需再等待一个列完成即可对列进行迭代。 如果您犯了错误，只需按几下按键即可进行更正 — 无需再等待两次更新完成后即可重新开始工作。

>[!IMPORTANT]
>
>使用SQL编辑器创建的列不会保存到Data warehouse中。 您始终可以访问包含列的查询，但如果您要在多个报表中使用列，则必须在每个报表的查询中重新创建该列。 这意味着使用SQL编辑器创建的列不能在传统中使用 `Report Builder`.

## data warehouse管理器中的列

列取决于更新周期，因此必须先完成一个完整的周期，然后才能对其进行编辑。 这些列将保存到Data warehouse管理器中，并可在传统模板中使用 `Report Builder` 或 `SQL Report Builder`.
