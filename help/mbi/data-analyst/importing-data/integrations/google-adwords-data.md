---
title: 预期的Google Adwords数据
description: 了解如何使用Data warehouse管理器轻松地跟踪相关数据字段以供分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 预期的Google Adwords数据

晚于 [您已连接 [!DNL Google Adwords] 帐户](../integrations/google-adwords.md)，您可以使用 [data warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段以供分析。

在该处，您注意到两个表格可用于复制到Data warehouse中： `campaigns[account-id]` 和 `adwords[account-id]`.

此 `campaigns` 表 *默认使用*，以便您可以开始同步该表中的所有相关字段。

此 `adwords` 表包含四列，这些列不在 `campaigns` 表：

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

只要您想执行考虑这些属性的分析，就必须使用 `adwords` 表格。

>[!IMPORTANT]
>
>此表排除了所有四列为 `null`.

以下是两个表的预期模式：

## `Campaigns` 表

此 `campaigns` 表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 当天的点击总数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 当天营销活动的总成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 营销活动ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促销活动名称(例如， [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 配置文件ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 此行上次更新的日期和时间 |

{style="table-layout:auto"}

## AdWords表

此 `adwords` 表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 当天的点击总数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 当天营销活动的总成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 营销活动ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促销活动名称(例如， [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 配置文件ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 此行上次更新的日期和时间 |
| `keyword` | 营销活动关键词 |
| `adContent` | 在线营销活动文本的第一行 |
| `adDestinationUrl` | 要访问的URL [!DNL Adwords] 广告引用的流量 |
| `adGroup` | 的名称 [!DNL Adwords] 广告组 |

{style="table-layout:auto"}

使用此数据，您可以开始创建 [量度 ](../../../data-user/reports/ess-manage-data-metrics.md) 和 [报告](../../../tutorials/using-visual-report-builder.md) 基于支出数据和 [将其与您的终生收入结合起来以计算ROI](../../analysis/roi-ad-camp.md).

## 统一表

Adobe建议创建 `consolidated ad spend` 表将所有广告源中的数据合并到一个表中。 这使您能够使用一组指标进行广告分析。

如果没有统一表格，如果您在 `adwords` 表，您需要复制报表或创建重复的量度以将该数据与您的 [!DNL Facebook Ads] 数据。 使用统一表可以无缝地整合 [!DNL Facebook Ads] 使用您的现有数据 [!DNL Adwords] 报告。 您还可以按广告平台进行分段。

如果您已同步上述字段，请联系我们以整合您的广告支出。
