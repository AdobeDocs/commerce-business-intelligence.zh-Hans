---
title: 预期的Facebook Ads数据
description: 了解建议同步到Data warehouse的表的简要概述
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 预期 [!DNL Facebook Ads] 数据

在您拥有 [已连接 [!DNL Facebook Ads] 帐户](../integrations/facebook-ads.md)，您可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段以供分析。

本主题简要概述了Adobe建议您同步到Data warehouse的表。 这仅突出显示核心表，因为有许多子表。

## 核心广告营销活动表

这些表包含有关核心广告促销活动组件的数据。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表是中促销活动的核心表 [!DNL Facebook Ads] 帐户。 列包括 `campaign id`， `name`， `status (active/paused)`， `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此表记录是以下项目的核心表： [!DNL Facebook Ads] 在中设置 [!DNL Facebook Ads] 帐户。 列包括广告 `Campaign id/name` 广告集属于、预算、竞价类型、计划和受众定位信息。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表记录了 [!DNL Facebook Ads] 帐户。 列包括广告信息，包括广告集及其所属的广告营销活动、广告投标、广告定位以及广告使用的特定创意（图像/文本）引用。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

此表记录以下项目中使用的创意： [!DNL Facebook Ads]. 创意内容包括创意名称、描述以及适用的相关图像URL。

## 分段营销活动表

下表包含每天每个促销活动/集/广告组合的条目，并按维度（如年龄、性别和国家/地区）分段。

### `facebook _ads insights_ (account-id)`

此表包括每天每个促销活动/集/广告组合的条目，以及包括展示次数、点击次数、成本、cpc、cpm、cpp、ctr、覆盖率、社交范围和支出在内的统计数据。

### `facebook _ads insights_ (account-id)_~\_actions`

这是 `facebook_ads_insights_{account_id}` 表格。 它包括根据不同营销活动发生的操作的转化数据。

### `facebook _ads insights country_ (account-id)`

此表包含的信息与 `facebook_ads_insights_{account_id}` 表格并按国家/地区进行细分。

### `facebook ads insights age and gender (account-id)`

此表包含的信息与 `facebook_ads_insights_{account_id}` 表格和按年龄和性别分列。

## 相关

* [正在连接 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
