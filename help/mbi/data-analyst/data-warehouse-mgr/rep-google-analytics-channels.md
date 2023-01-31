---
title: 使用客户获取源复制Google Analytics渠道
description: 了解如何使用客户获取源复制Google Analytics渠道。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Google Analytics使用客户获取源

## 什么是渠道？ {#channels}

创建自定义区段，以查看不同流量的表现和观察趋势（好坏！） 是  [!DNL Google Analytics ]. 默认存在于 [!DNL Google Analytics ] are `Channels`. 渠道是人们访问您网站的常用方式分组。  [!DNL Google Analytics ] 自动对您获取用户的多种方式（无论是社交媒体、每次点击付费、电子邮件还是反向链接）进行排序，并将它们捆绑到存储段或渠道中。

## 为什么我看不到 `channels` 在MBI中？ {#nochannels}

`Channels` 是简单的数据聚合桶。 要将您的客户获取排序到渠道存储段中，Google会使用特定参数设置不同的规则和定义：收购组合 [来源](https://support.google.com/analytics/answer/1033173?hl=en) （流量的来源）和客户获取 [中](https://support.google.com/analytics/answer/6099206?hl=en) （源的一般类别）。

虽然拥有这些存储段可以帮助您了解流量的来源，但此数据实际上并非由渠道标记，而是由源和媒体的组合标记。 由于Google将渠道信息作为两个单独的数据点发送，因此渠道分组不会自动显示在 [!DNL MBI].

## 默认的渠道分组是什么？ 它们是如何创建的？

默认情况下，Google会为您设置8个不同的渠道。 让我们看一看确定如何创建规则的规则：

| 渠道 | 这是什么？ | 它是如何创建的？ |
|---|---|---|
| 直接 | 直接进入您网站的任何人。 | 来源= `Direct`<br>和中= `(not set); OR Medium = (none)` |
| 自然搜索 | 在无报酬搜索引擎中自然排名的流量。 | 中= `organic` |
| 反向链接 | 来自非自然搜索外部链接或来自非社交网络网站的流量。 | 中= `referral` |
| 付费搜索 | 具有UTM跟踪代码的流量，其中媒体为“cpc”、“ppc”或“paidsearch”，并且是与“内容”不匹配的广告分发网络。 | 中= `^(cpc|ppc|paidsearch)$`<br>和广告分发网络≠ `Content` |
| 社交 | 来自以下任何 [400个社交网络](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 和未标记为广告。 | 社交来源反向链接= `Yes`<br>或中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 电子邮件 | 以“电子邮件”为媒介标记的会话的流量。 | 媒体的UTM跟踪代码= `email` |
| 显示 | 具有UTM跟踪代码且媒体为显示或cpm的流量。 还包括广告分发网络与“内容”匹配的AdWords交互 | 中= `^(display|cpm|banner)$`<br>或广告分发网络= `Content`<br>AND广告格式≠ `Text` |
| 其他 | 来自其他广告渠道（不包括付费搜索）的会话，这些渠道以“cpc”、“ppc”、“cpm”、“cpv”、“cpp”、“cpp”、“附属活动”等媒介进行标记。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## 如何在我的Data warehouse中重新创建这些渠道分组？ {#recreate}

既然您知道渠道只是源和媒介的组合，那么在您的Data warehouse中重新创建这些分组就是一个简单的3步流程。

1. **启用[!DNL Google ECommerce]集成**

   [启用后](../importing-data/integrations/google-ecommerce.md)，请确保 [同步](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **媒体** 和 **来源** 字段。 完成后，中和源客户获取数据将引入您的Data warehouse。

1. **上传Google渠道分组的映射**

   为了节省您的时间，Commerce已经创建了一个表，其中默认分组映射为一个文件，您可以 [下载](../../assets/ga-channel-mapping.csv).

   如果您是Google Analytics专业人员并创建了自己的渠道，则需要先将特定规则添加到映射表中，然后再将文件上传到 [!DNL MBI].

   将其作为 [文件上传](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **在[!DNL Google ECommerce]和映射文件上传**

   在[!DNL Google ECommerce]和映射表， [提交支持请求](../../guide-overview.md) 敬请我们的数据分析团队，并参考本文。 分析师将创建一个新的计算列，名为 **渠道** 中。 **完整更新周期后**，此列将可在过滤器或分组依据中使用。

恭喜！ 现在，您的Data warehouse中包含Google Analytics渠道分组，这意味着您可以从新的角度分析数据：

![按渠道划分订单数量量度](../../assets/GA_Channel_Gif.gif)

在此示例中，我们开始简单 — 对 **订单数** 量度 **渠道**. 现在轮到您了 — 测试新列，并查看您能够在Google Analytics渠道数据中识别的趋势！

## 相关文档

* [使用Report Builder](../../tutorials/using-visual-report-builder.md)
* [预期[!DNL Google ECommerce]数据](../importing-data/integrations/google-ecommerce-data.md)
* [建筑[!DNL Google ECommerce]包含订单和客户数据的维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [您最有价值的客户获取来源和渠道是什么？](../analysis/most-value-source-channel.md)
