---
title: 使用客户获取源复制Google Analytics渠道
description: 了解如何使用客户获取源复制Google Analytics渠道。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] 使用客户获取源

## 什么是渠道？ {#channels}

创建自定义区段以查看不同流量的表现和观察趋势，是功能最强大的用途之一 [!DNL Google Analytics]. 中默认存在的一类区段 [!DNL Google Analytics] 是 `Channels`. 渠道是用户访问您网站的一组常用方式。  [!DNL Google Analytics] 自动对您获取用户的多种方式进行排序（无论是社交媒体、每次点击付费、电子邮件还是推荐链接），并将其捆绑到存储桶或渠道中。

## 为什么我看不到我的 `channels` 在Commerce Intelligence中？ {#nochannels}

`Channels` 是简单的聚合数据桶。 要将您的客户获取分类到渠道存储桶中， [!DNL Google] 使用特定参数设置不同的规则和定义：客户获取组合 [来源](https://support.google.com/analytics/answer/1033173?hl=en) （流量的来源）和客户获取 [中](https://support.google.com/analytics/answer/6099206?hl=en) （源的一般类别）。

虽然拥有这些存储段可以帮助您了解流量的来源，但此类数据不会按渠道进行标记，而是按源和媒体的组合进行标记。 因为 [!DNL Google] 将渠道信息作为两个单独的数据点发送，渠道分组不会自动显示于 [!DNL Commerce Intelligence].

## 默认渠道分组是什么？ 它们是如何创建的？

默认情况下， [!DNL Google] 设置了八个不同的渠道。 确定如何创建渠道的规则如下所示。

| **渠道** | **这是什么？** | **它是如何创建的？** |
|---|---|---|
| 直接 | 直接进入您网站的任何人。 | 源= `Direct`<br>和中= `(not set); OR Medium = (none)` |
| 自然搜索 | 在无偿搜索引擎中已自然排名的流量。 | 中= `organic` |
| 反向链接 | 来自非自然搜索外部链接或非社交网络网站的流量。 | 中= `referral` |
| 付费搜索 | 具有UTM跟踪代码的流量，其中媒体为“cpc”、“ppc”或“paidsearch”，并且是不匹配“Content”的广告分发网络。 | 中= `^(cpc|ppc|paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | 来自以下任何一项的引荐流量： [400个社交网络](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 和未被标记为广告。 | 社交源反向链接= `Yes`<br>或中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 电子邮件 | 使用“电子邮件”媒介标记的会话流量。 | Medium的UTM跟踪代码= `email` |
| 显示 | 具有UTM跟踪代码（媒体为显示或cpm）的流量。 此外，还包括广告分发网络与“内容”匹配的AdWords交互 | 中= `^(display|cpm|banner)$`<br>或Ad分发网络= `Content`<br>AND广告格式≠ `Text` |
| 其他 | 来自使用“cpc”、“ppc”、“cpm”、“cpv”、“cpa”、“cpp”、“affiliate”媒介标记的其他广告渠道（不包括付费搜索）的会话。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## 如何在Data Warehouse中重新创建这些渠道分组？ {#recreate}

现在您知道渠道只是源和媒介的组合，只需分三步即可在Data Warehouse中重新创建这些分组。

1. **启用您的[!DNL Google ECommerce]集成**

   [启用时](../importing-data/integrations/google-ecommerce.md)，确保 [同步](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **中** 和 **源** Data Warehouse中的字段。 完成此操作后，介质和源获取数据将引入您的Data Warehouse。

1. **上传Google渠道分组的映射**

   Adobe Commerce创建一个表，并将默认分组映射为文件，您可以 [下载](../../assets/ga-channel-mapping.csv).

   如果您是 [!DNL Google Analytics] 创建自己的渠道后，您想要在将文件上传到之前将特定规则添加到映射表 [!DNL Commerce Intelligence].

   将它作为a引入您的Data Warehouse [文件上传](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **建立以下两项之间的关系：[!DNL Google ECommerce]和映射文件上传**

   要建立[!DNL Google ECommerce] 和映射表， [提交支持请求](../../guide-overview.md#Submitting-a-Support-Ticket) 敬请咨询您的数据分析师团队并参考此主题。 分析人员将创建一个新的计算列，名为 **渠道** 在电子商务表格中。 **经过一个完整的更新周期后**，此列将可以在 `Filter` 或 `Group by`.

您现在拥有 [!DNL Google Analytics Channel] Data Warehouse中的分组，这意味着您可以从新的角度分析数据：

![按渠道对“订单数”量度进行分段](../../assets/GA_Channel_Gif.gif)

在此示例中，您开始了简单的分段 **订单数** 量度依据 **渠道**. 测试您的新列，查看您可以在的新列中找出哪些趋势 [!DNL Google Analytics Channel] 数据！

## 相关文档

* [使用Report Builder](../../tutorials/using-visual-report-builder.md)
* [预期[!DNL Google ECommerce]数据](../importing-data/integrations/google-ecommerce-data.md)
* [正在生成[!DNL Google ECommerce]包含订单和客户数据的维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [您最宝贵的客户获取来源和渠道是什么？](../analysis/most-value-source-channel.md)
