---
title: 预期 [!DNL Adobe Analytics] 数据
description: 了解连接RDS实例的步骤。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# 预期 [!DNL Adobe Analytics] 数据

的 [!DNL Adobe Analytics] 集成 [!DNL MBI] 使用 [Analytics 2.0报表API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>为确保获得所需数据，您可以先在 [!DNL Adobe Analytics] 包含所需量度和维度的工作区。 这允许您检查数据的兼容性和可用性。

每个连接的报表包有一个表 — 称为 `report-suite-<ID>`，其中 `<ID>` 是由 [!DNL MBI]  — 将在您的Data warehouse中创建。

此表的架构由您在集成设置过程中选择的量度和维度组成。 还会生成其他几个列 [!DNL MBI]，用于标识。

例如，如果您在设置过程中选择了以下量度和维度：
- `Metric`: `Page views`
- `Dimension`: `Page`

表将包含以下列：

| 列名称 | 描述 |
| --- | --- |
| `_id` | 此列是主键。 |
| `_item_hash` | [!DNL MBI] 唯一标识符。 此列由 [!DNL MBI]. |
| `_updated_at` | 此列包含数据行上次更新的时间。 创建者 [!DNL MBI]. |
| `start_date` | 行的包含数据的开始日期。 `start_date` 将始终为同一天的00:00。 |
| `end_date` | 行的包含数据的结束日期。 `end_date` 将始终是同一天的23:59。 |
| `page_views` | 选定量度：已识别时间段内的页面查看总数。 |
| `page` | 所选维度：具有跟踪视图的单个页面名称。 |

控制哪些选定量度和维度在您的 [!DNL MBI] 表 *同步* 或 *取消同步* 选项 `Data Warehouse` 页面。 当前未同步的列以灰色显示。 如果您停止同步列，则可以稍后再次开始同步该列。

## 当前限制

本节概述了 [!DNL Adobe Analytics] 集成 [!DNL MBI].

| 限制 | 描述 |
| --- | --- |
| `Historical data period` | 与其他第三方集成一样， [!DNL Adobe Analytics] 集成会提取有限数量的历史数据，然后继续保持数据更新。 历史时段配置为2周。 |
| `Empty component combinations` | 一些量度和维度组合不包含任何数据。 如果选择此组合进行复制， [!DNL MBI] 从复制表中排除列。 为避免选择此类组合，您可以先在 [[!DNL Adobe Analytics] 工作区](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) 以验证您是否会获得所需数据。 |
| `Re-authorization cadence` | 重新授权 [!DNL Adobe Analytics] 目前，每两周需要一次集成。 要重新授权，请转到集成的编辑页面，然后单击 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 一次提供一个维度的量度数据。 如果在设置期间选择多个维度，则 [!DNL MBI] 表将包含一个维度值和每个其他维度的空值。 |
