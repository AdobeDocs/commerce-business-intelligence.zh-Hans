---
title: 预期的Google Adwords数据
description: 了解如何使用Data Warehouse Manager轻松地跟踪相关数据字段以供分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iCKOCRAELybmKfHS8F7XaKpEx9blpkRK0i0e-eEYJgU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# 预期[!DNL Google Adwords]数据

在连接[您的 [!DNL Google Adwords] 帐户](../integrations/google-adwords.md)后，您可以使用[Data Warehouse管理器](../../data-warehouse-mgr/tour-dwm.md)轻松跟踪相关数据字段以供分析。

您在该处注意到两个可用于复制到Data Warehouse中的表：

* `campaigns[account-id]`
* `adwords[account-id]`

默认情况下应使用`campaigns`表&#x200B;*，因此您可以从该表开始同步所有相关字段。*

`adwords`表包含不在`campaigns`表中的四个列：

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

只要您想执行考虑这些属性的分析，就必须使用`adwords`表。

>[!IMPORTANT]
>
>此表不包括所有四列均为`null`的行。

以下是两个表的预期模式。

## [!DNL Campaigns]表

`campaigns`表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 当天的点击总数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 当天营销活动的总成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords]营销活动ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 营销活动名称（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 用户档案ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 此行上次更新的日期和时间 |

{style="table-layout:auto"}

## [!DNL AdWords]表

`adwords`表包含以下列：

| **列** | **描述** |
|-----|-----|
| `\_id` | 表的主键 |
| `accountId` | 帐户ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 当天的点击总数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 当天营销活动的总成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords]营销活动ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 营销活动名称（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 营销活动运行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 当天的展示次数 |
| `profileId` | 用户档案ID |
| `profileName` | 配置文件名称 |
| `\_updated\_at` | 此行上次更新的日期和时间 |
| `keyword` | 营销活动的关键词 |
| `adContent` | 在线营销活动文本的第一行 |
| `adDestinationUrl` | [!DNL Adwords]广告引用流量的URL |
| `adGroup` | [!DNL Adwords]广告组的名称 |

{style="table-layout:auto"}

使用此数据，您可以开始根据支出数据创建[量度](../../../data-user/reports/ess-manage-data-metrics.md)和[报告](../../../tutorials/using-visual-report-builder.md)，并[将其与您的生命周期收入结合以计算ROI](../../analysis/roi-ad-camp.md)。

## 统一表

[!DNL Adobe]建议创建一个`consolidated ad spend`表以将来自您所有多个广告源的数据合并到一个表中。 这使您能够将一组量度用于广告分析。

如果您没有合并表，并且在`adwords`表上构建了一个漂亮的仪表板，则需要复制报表或创建重复的量度以将该数据与您的[!DNL Facebook Ads]数据进行比较。 通过使用合并表，您可以将[!DNL Facebook Ads]数据无缝地合并到您现有的[!DNL Adwords]报表中。 您也可以按广告平台进行分段。

如果您已同步上述字段，请[联系我们](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以整合您的广告支出。
