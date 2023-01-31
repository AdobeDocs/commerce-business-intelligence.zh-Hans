---
title: 预期的Google Adwords数据
description: 了解如何使用Data warehouse管理器轻松跟踪相关数据字段以进行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 预期的Google Adwords数据

之后 [您已连接 [!DNL Google Adwords] 帐户](../integrations/google-adwords.md)，则可以使用 [data warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。

在此，您注意到有两个表可用于复制到data warehouse中： `campaigns[account-id]` 和 `adwords[account-id]`.

的 `campaigns` 表 *默认情况下应使用*，以便您可以首先同步该表中的所有相关字段。

的 `adwords` 表包含四列不在 `campaigns` 表：

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

只要您有兴趣执行考虑这些属性的分析，就必须使用 `adwords` 表。

>[!IMPORTANT]
>
>此表将排除所有这四个列都包含在 `null`.

以下是两个表的预期模式：

## `Campaigns` 表

的 `campaigns` 表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 当天的总点击次数 |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 营销活动当天的总成本 |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 促销活动ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促销活动名称(例如， [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 配置文件ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 该行上次更新的日期和时间 |

{style=&quot;table-layout:auto&quot;}

## AdWords表

的 `adwords` 表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 当天的总点击次数 |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 营销活动当天的总成本 |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 促销活动ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促销活动名称(例如， [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 配置文件ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 该行上次更新的日期和时间 |
| `keyword` | 促销活动的关键词 |
| `adContent` | 在线营销活动的文本第一行 |
| `adDestinationUrl` | 指向的URL [!DNL Adwords] 广告引荐流量 |
| `adGroup` | 的名称 [!DNL Adwords] 广告组 |

{style=&quot;table-layout:auto&quot;}

使用此数据，您可以开始创建 [量度 ](../../../data-user/reports/ess-manage-data-metrics.md) 和 [报告](../../../tutorials/using-visual-report-builder.md) 根据支出数据和 [将其与您的终身收入相结合，以计算ROI](../../analysis/roi-ad-camp.md).

## 统一表

我们始终建议创建 `consolidated ad spend` 表格，将来自所有多个广告源的数据合并到一个表格中。 这样，您就可以使用一组量度进行广告分析。

如果没有统一表，则在 `adwords` 表中，您需要复制报表或创建重复的量度，以将该数据与您的 [!DNL Facebook Ads] 数据。 通过使用统一表，您可以无缝地合并 [!DNL Facebook Ads] 数据 [!DNL Adwords] 报表。 （别担心 — 您还可以按广告平台进行分段！）

如果您已同步上述字段，请联系我们以整合您的广告支出。
