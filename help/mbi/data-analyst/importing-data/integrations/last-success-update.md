---
title: 了解数据库和SQL编辑器之间的结果
description: 了解数据库和SQL编辑器之间的结果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 数据库结果与 `SQL Editor` 结果

你可能会好奇 `Last successful update began` 字段在您的 `Integrations` 页面：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 了解 `timestamp` 字段

它显示了开始 `timestamp` （在您帐户设置的时区内） _上次成功更新周期_ 在您的帐户上。

- 如果任何同步的表在上次更新周期遇到问题，则此时间戳为 *未更新*.
- 因此，在某些情况下，报告可能更新了新数据，但 *上次成功更新已开始* 仍然落后。

## 确定“真正的”最后一个数据点

特定集成的最新数据点由 `Last Data Point Received` `timestamp` 位于每个集成的右侧。 该时间戳是指您的Data warehouse从数据源成功接收数据点的最后一个时间点，无论数据点是数据库、API还是第三方集成。

检查来自以下位置的数据的时效性： *特定表*，Adobe建议快速创建 [SQL报告](../../dev-reports/sql-rpt-bldr.md) 会执行 `MAX(timestamp)` 在您帐户中最重要的表格上。 将此时间戳与 `Last Data Point` 指示问题影响的是整个帐户还是表的子集。 Adobe建议对三到四个常用重要表执行此操作。

- 如果 `MAX(timestamp)` 值比 `Last Data Point Received`，这意味着一部分表受到影响，但整个帐户的更新周期是稳定的。
- 如果 `MAX(timestamp)` 值等于或早于 `Last Data Point Received`，这意味着帐户的更新周期受到影响。 在这种情况下， [提交支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
