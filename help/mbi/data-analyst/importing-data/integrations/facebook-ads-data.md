---
title: 预期的Facebook广告数据
description: 了解我们建议您同步到您的data warehouse的表的简要概述
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 预期 [!DNL Facebook Ads] 数据

![](../../../assets/Facebook_Logo.png)

在 [已连接 [!DNL Facebook Ads] 帐户](../integrations/facebook-ads.md)，则可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。

在本文中，我们简要概述了我们建议您同步到您的data warehouse的表。 这不是一个完整列表，因为有许多子表。 我们只强调核心表格。

## 核心广告促销活动表

这些表包含有关核心广告营销活动组件的数据。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

此表是 [!DNL Facebook Ads] 帐户。 列包括 `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此表记录是 [!DNL Facebook Ads] 在 [!DNL Facebook Ads] 帐户。 列包括广告 `Campaign id/name` 广告集属于的预算、竞价类型、计划和受众定位信息。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

此表记录 [!DNL Facebook Ads] 帐户。 列包括广告信息，包括广告集及其所属的广告促销活动、广告竞价、广告定位以及对广告所使用的特定创意（图像/文本）的引用。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

此表记录了 [!DNL Facebook Ads]. 这些URL包括创作名称、描述和相关的图像URL（如果适用）。

## 分段促销活动表

下表包含每天每个促销活动/集/广告组合的条目，按年龄、性别和国家/地区等维度进行分段。

### `facebook _ads insights_ (account-id)`

此表包括每天每个促销活动/集/广告组合的条目，以及包括展示次数、点击次数、成本、cpc、cpp、cpp、ctr、访问、社交访问和支出在内的统计信息。

### `facebook _ads insights_ (account-id)_~\_actions`

这是 `facebook_ads_insights_{account_id}` 表。 它包含根据不同营销活动执行的操作的转化数据。

### `facebook _ads insights country_ (account-id)`

此表包含与 `facebook_ads_insights_{account_id}` 按国家/地区对其进行表格和细分。

### `facebook ads insights age and gender (account-id)`

此表包含与 `facebook_ads_insights_{account_id}` 按年龄和性别对表格进行划分。

## 相关

* [连接 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
