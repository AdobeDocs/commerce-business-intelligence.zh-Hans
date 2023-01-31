---
title: Google Analytics和UTM归因
description: 了解Google Analytics源归因流程。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics和UTM归因

这对 [跟踪用户获取源](../../data-analyst/analysis/google-track-user-acq.md) to [确定效果最佳的广告促销活动](../../data-analyst/analysis/most-value-source-channel.md). 在本教程中，我们将探索Google Analytics源归因流程。 换句话说，在记录什么信息时。

## 什么是归因？

`Attribution` 是关于指定特定活动的反向链接源。 这些活动通常是宏转化或微转化，宏观是指 **购买**，微生物 **注册、电子邮件注册、博客评论、** 等等。

理想情况下，每次发生转化事件时，都会记录反向链接源。 但消息来源如何确定？

现实情况是，用户在点击/提交微观或宏观转化之前，通常会从多个来源获得（例如，他们可能通过自然方式访问网站，离开，通过付费搜索，离开，然后直接访问网站本身）。 此源跟踪信息通常通过UTM参数提供给网站，但其中也有更复杂的系统。 为我们的目的，我们将重点 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 如何 [!DNL Google Analytics] 是否通过UTM参数来提供引荐源属性？

当在URL上指定UTM参数时，会将这些参数解析出并放置到 [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). 如果网站没有 [!DNL Google Analytics]，则使用UTM没有意义。 [!DNL Google Analytics] 有一些规则，用于规定如何处理在生命周期中（稍后会详细介绍）通过UTM点击多个URL的用户。 假设网站配置为将UTM参数捕获到外部数据库中，则无论在 [!DNL Google Analytics] cookie在转换时将被复制到数据库。

## 首次点击与最后点击

### 上次点击归因

最后点击归因是 [!DNL Google Analytics]. 在本例中， [!DNL Google Analytics] cookie表示转化事件之前最后一个或最近一个源的UTM参数，这就是 [记录在数据库中](../../data-analyst/analysis/google-track-user-acq.md). 请注意， [!DNL Google Analytics] 仅当用户单击包含一组新UTM参数的新URL时，Cookie才会覆盖之前的UTM参数。

例如，假定用户是首次通过 [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *付费搜索*，然后返回 *自然搜索*，最后返回到 *直接* 或通过 *电子邮件链接* **不包含UTM参数** 在转化事件之前。 在本例中， [!DNL Google Analytics] cookie表示用户的源是自然的，因为这表示转化前的最后一个源。 的 *路径* 将忽略最终转化事件之前用户的URL。 相反，如果用户通过带有UTM的电子邮件链接访问了网站，则 [!DNL Google Analytics] cookie会表示来源为“电子邮件”。 因此，如果Cookie中存在现有UTM参数，且用户通过直接进入，则 [!DNL Google Analytics] cookie将始终显示UTM参数，而不是“直接”。

>[!NOTE]
>
>特定用户的 [!DNL Google Analytics] cookie参数将在cookie [过期](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)，或用户在浏览器中清除其cookie时。*)

### 首次点击归因

某些付费归因工具将允许您捕获用户路径中源的“煎饼堆”。 在这种情况下，在上例中，首次点击归因将告诉我们付费搜索。 或者，少数网站会实施自己的Cookie，以捕获煎饼堆并将第一个源存储到其数据库中。

## 如何分析归因？

[!DNL Google Analytics] 其web界面中有一些更强大的功能，允许您执行四种不同的归因模型：首次点击、最后点击、线性（在路径中所有来源之间均等划分收入）以及加权（自定义归因）。

既然您了解了每个微观或宏观转化的归因模型是什么，那么接下来的问题就是您如何处理用户转化总数？  例如，查看根据GA上次点击逻辑记录的UTM:

* 用户在免费下注册
* 付费搜索下用户的首次购买$5.00
* 用户在电子邮件下第二次购买的费用为$50.00
* 用户在免费价格10.00美元下的第三次购买

下面是您问的问题：我通过付费搜索获得了多少收入？  从电子邮件？  有机的？  你可以说答案是5、50和10（即，不管最后一个来源是什么），或者你也可以说将所有收入都归因于第一个来源（即所有65个都归自然来源）。 您还可以应用一些加权分析或应用线性模型（即每个约22个）。

## 相关文档

* [通过跟踪订单反向链接来源 [!DNL Google Analytics] 电子商务](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../analysis/google-track-user-acq.md)
* [发现最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [提高广告活动的ROI](../analysis/roi-ad-camp.md)
* [在 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
