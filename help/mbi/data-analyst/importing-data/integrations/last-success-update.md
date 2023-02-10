---
title: 了解数据库和SQL编辑器之间的结果
description: 了解数据库和SQL编辑器之间的结果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 数据库结果与 `SQL Editor` 结果

你可能很好奇 `Last successful update began` 字段 `Integrations` 页面：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 了解 `timestamp` 字段

它显示开始 `timestamp` （在您帐户设置的时区中） _上次成功更新周期_ 你的账户。

- 如果任何已同步的表在上次更新周期中遇到问题，则此时间戳为 *未更新*.
- 因此，在某些情况下，报表可能会更新为新数据，但 *上次成功更新开始* 仍然滞后。

## 确定“真实”的最后一个数据点

特定集成的最新数据点由 `Last Data Point Received` `timestamp` 位于每个集成的右侧。 该时间戳是指您的data warehouse成功从该源接收数据点（无论是数据库、API还是第三方集成）的最后一个时间点。

要检查 *特定表*，我们建议创建快速 [SQL报告](../../dev-reports/sql-rpt-bldr.md) 执行 `MAX(timestamp)` 在您帐户中最重要的表格上。 将此时间戳与 `Last Data Point` 将指示问题是影响整个帐户还是表的子集。 我们建议对三到四个常用的重要表执行此操作。

- 如果 `MAX(timestamp)` 值比 `Last Data Point Received`，这表示部分表受到影响，但整个帐户的更新周期是稳定的。
- 如果 `MAX(timestamp)` 值等于或早于 `Last Data Point Received`，则表示帐户的更新周期受到影响。 在这种情况下， [提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
