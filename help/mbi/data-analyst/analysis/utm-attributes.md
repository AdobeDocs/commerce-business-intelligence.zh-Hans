---
title: Google Analytics和UTM归因
description: 了解Google Analytics源归因流程。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics]和UTM归因

[跟踪用户获取来源](../../data-analyst/analysis/google-track-user-acq.md)对于[识别表现最佳的广告营销活动](../../data-analyst/analysis/most-value-source-channel.md)至关重要。 本主题探讨[!DNL Google Analytics]源归因过程。 换言之，何时记录哪一条信息。

## 什么是归因？

`Attribution`用于指定特定活动的引用源。 这些活动通常是宏观转化或微观转化，宏观是&#x200B;**购买**&#x200B;之类的内容，微观是&#x200B;**注册、电子邮件注册、博客评论**&#x200B;之类的内容。

理想情况下，每次发生转化事件时，都会记录反向链接来源。 但如何确定来源？

实际上，用户通常在点击/进行微观或宏观转化之前来自许多来源。 例如，他们可能通过有机方式访问网站，然后离开，然后通过付费搜索访问，然后离开，然后直接访问网站本身。 此源跟踪信息通常通过UTM参数提供给站点，但也有更复杂的系统。 出于您的目的，请关注[UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998)。

## [!DNL Google Analytics]如何通过UTM参数确定反向链接来源？

在URL上指定UTM参数后，这些参数会被解析并置于[!DNL Google Analytics] [Cookie](https://en.wikipedia.org/wiki/HTTP_cookie)中。 如果网站没有[!DNL Google Analytics]，则使用UTM没有任何意义。 [!DNL Google Analytics]具有如何处理在其生命周期内点击多个URL且带有UTM的用户（稍后将详加介绍）的规则。 假设网站配置为将UTM参数捕获到外部数据库中，那么当发生微或宏转换时，转换时[!DNL Google Analytics] Cookie中的任何内容都会被复制到数据库中。

## 首次点击与最后点击

### 最后点击归因

最后点击归因是[!DNL Google Analytics]使用的最常见归因模型。 在本例中，[!DNL Google Analytics] Cookie表示转换事件之前的最新源的UTM参数，该参数在数据库[中记录为](../../data-analyst/analysis/google-track-user-acq.md)。 如果用户单击包含新UTM参数集的新URL，[!DNL Google Analytics] Cookie仅会覆盖以前的UTM参数。

例如，假定某个用户首先通过[!DNL Google Analytics] *付费搜索*&#x200B;访问网站，然后通过&#x200B;*免费搜索*&#x200B;返回，最后在转化事件之前直接返回&#x200B;*网站*&#x200B;或通过&#x200B;*电子邮件链接* **返回，而不使用UTM参数**。 在此示例中，[!DNL Google Analytics] Cookie显示用户的源是有机的，因为这是转换前的最后一个源。 忽略最终转化事件之前的用户的&#x200B;*路径*。 如果用户改为通过带有UTM的电子邮件链接访问网站，则[!DNL Google Analytics] Cookie将表明源是“电子邮件”。 因此，如果Cookie中存在UTM参数，并且用户通过直接进入，则[!DNL Google Analytics] Cookie会显示UTM参数，而不是“直接”。

>[!NOTE]
>
>当Cookie [!DNL Google Analytics]过期[或用户在浏览器中清除其Cookie时，特定用户的](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage) Cookie参数将被清除。*

### 首次点击归因

某些付费归因工具允许您在用户路径中捕获来源的“蛋糕栈”。 在这种情况下，在上述示例中，首次点击归因将告知我们付费搜索。 或者，一些网站实施自己的Cookie，以捕获饼栈并将第一个源存储到其数据库中。

## 如何分析归因？

[!DNL Google Analytics]的Web界面具备一些强大的功能，可让您执行四种不同的归因模型：

1. 首次点击
1. 最后点击
1. 线性（将收入平均分配到路径中的所有源）
1. 加权（自定义归因）

现在您了解了每个微观或宏观转化的归因模型后，问题变成了“您如何处理用户转化的总体？”  例如，查看基于GA最后点击逻辑记录的UTM：

* 用户在Organic下注册
* 用户在付费搜索下的首次购买$5.00
* 用户通过电子邮件第二次购买了$50.00
* 用户第三次购买有机费$10.00

你问：“付费搜索给我多少收入？ 来自电子邮件？  还是有机的？” 您可以说，答案是5、50和10（无论最后一个来源是什么），或者您也可以说，您将所有收入归因于第一个来源（所有65个都归因于有机来源）。 您也可以应用某些加权分析或线性模型（即每个模型大约22个）。

## 相关文档

* [通过 [!DNL Google Analytics] E-Commerce跟踪订单反向链接来源](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../analysis/google-track-user-acq.md)
* [了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接你的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [提高广告促销活动的ROI](../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics]中UTM标记的五个最佳实践](../../best-practices/utm-tagging-google.md)
