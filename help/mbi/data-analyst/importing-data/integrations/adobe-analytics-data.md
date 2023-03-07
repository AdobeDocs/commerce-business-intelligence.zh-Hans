---
title: 预期 [!DNL Adobe Analytics] 数据
description: 了解连接RDS实例的步骤。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 预期 [!DNL Adobe Analytics] 数据

此 [!DNL Adobe Analytics] 集成 [!DNL MBI] 使用 [Analytics 2.0报表API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>为确保您获得所需数据，您可以首先在中构建报表 [!DNL Adobe Analytics] 包含所需量度和维度的工作区。 这允许您检查数据的兼容性和可用性。

每个连接的报表包一个表 — 称为 `report-suite-<ID>`，其中 `<ID>` 是由生成的唯一ID [!DNL MBI]  — 在您的Data warehouse中创建。

此表的架构由您在集成设置过程中选择的量度和维度组成。 还生成了其他多个列 [!DNL MBI]，用于标识目的。

例如，如果在设置期间选择了以下量度和维度：
- `Metric`: `Page views`
- `Dimension`: `Page`

该表将包含以下列：

| 列名称 | 描述 |
| --- | --- |
| `_id` | 此列是主键。 |
| `_item_hash` | [!DNL MBI] 唯一标识符。 此列的创建者 [!DNL MBI]. |
| `_updated_at` | 此列包含上次更新数据行的时间。 创建者 [!DNL MBI]. |
| `start_date` | 行所包含数据的开始日期。 `start_date` 始终为一行中的当天00:00。 |
| `end_date` | 行所包含数据的结束日期。 `end_date` 始终为一行中当天的23:59。 |
| `page_views` | 所选量度：已识别的时段内页面查看的总数。 |
| `page` | 选定的维度：具有跟踪视图的单个页面名称。 |

控制哪些选定的量度和维度在您的 [!DNL MBI] 表，通过使用 *同步* 或 *取消同步* 中的选项 `Data Warehouse` 页面。 当前未同步的列以灰色显示。 如果停止同步列，可以稍后再次开始同步。

## 当前限制

本节概述了 [!DNL Adobe Analytics] 集成 [!DNL MBI].

| 限制 | 描述 |
| --- | --- |
| `Historical data period` | 与其他第三方集成一样， [!DNL Adobe Analytics] 集成会提取有限数量的历史数据，然后继续保持数据更新。 历史时段配置为2周。 |
| `Empty component combinations` | 某些量度和维度组合不包含数据。 如果选择这种组合进行复制， [!DNL MBI] 从复制表中排除列。 要避免选择此类组合，您可以首先在 [[!DNL Adobe Analytics] 工作区](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) 来验证您是否获得了预期的数据。 |
| `Re-authorization cadence` | 重新授权 [!DNL Adobe Analytics] 每两周需要集成一次。 要重新授权，请转到集成的“编辑”页面并单击 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 一次提供一个维度的量度数据。 如果在设置期间选择多个维，则在 [!DNL MBI] 表包含单个维度值，且每个维都为null。 |
