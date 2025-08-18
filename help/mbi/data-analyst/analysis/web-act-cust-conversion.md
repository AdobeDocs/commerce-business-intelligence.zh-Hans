---
title: 分析网站活动和客户转化率
description: 了解如何设置一个功能板来跟踪您的网站活动（包括页面查看次数、会话数和用户），以及客户在一段时间内的转化率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 分析网站活动

[!DNL Adobe Commerce Intelligence]允许您轻松地将广告成本数据与您的其余数据集成。 这不仅使您能够了解网站活动，而且使您能够推导出网站上成为注册用户或进行购买的访客百分比。

本主题将演示如何设置一个功能板，用于跟踪您网站的活动（包括页面查看次数、会话数和用户）以及一段时间内您的客户转化率。

## 先决条件

**导入您的广告成本数据** — 将[!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md)连接到[!DNL Adobe Commerce Intelligence] — 这会自动同步您在Commerce Intelligence中的[!DNL AdWords]支出。

**跟踪用户获取渠道数据** — 若要将[!DNL Google AdWords]数据与数据库中的特定订单绑定，必须[通过](../analysis/google-track-user-acq.md)跟踪用户获取[!DNL Google Analytics E-commerce]。 这样，您就可以将每个订单与utm源和媒介连接。

## 用户获取促销活动

此报表的集合使用以下项目构建：

* 连接[!DNL Google AdWords]数据时自动生成的量度
* 您的帐户中应已可用的基本量度，如`Number of orders`和`New users`
* 将[!DNL Google Analytics Ecommerce]数据加入数据库时创建的维度，如订单的utm源和订单的utm介质。 如果您的帐户中当前没有这些字段，请联系支持团队

## 构建报告

**首先，创建一个显示一段时间内页面查看次数、会话数和用户数的报告：**

1. 创建报告。
1. 单击&#x200B;**[!UICONTROL Add Metric]**，然后将鼠标悬停在下拉列表底部的[!DNL Google Analytics]部分上并选择`Page Views`。
1. 添加另一个量度，再次悬停在[!DNL Google Analytics]部分中，这次选择`Sessions`。
1. 添加第三个量度，再次悬停在[!DNL Google Analytics]部分中，这次选择`Users`。
1. 现在将您的时间段更改为移动范围（从31天前到1天前），并将时间间隔调整为`by day`。
1. 为您的报表命名（例如，`Page views, sessions and users by day`），然后单击&#x200B;**[!UICONTROL Save]**。

**第二个报表查看过去一年中的页面查看次数：**

1. 创建报告。
1. 单击&#x200B;**[!UICONTROL Add Metric]**，将鼠标悬停在下拉列表底部的[!DNL Google Analytics]部分上并选择&#x200B;_页面查看次数_。
1. 将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为`by month`。
1. 为您的报告提供一个名称（如`Page views by month,`），然后单击&#x200B;**[!UICONTROL Save]**。

**第三个图表查看过去一年中的跳出率：**

1. 创建报告。
1. 单击&#x200B;**[!UICONTROL Add Metric]**，将鼠标悬停在下拉列表底部的[!DNL Google Analytics]部分上并选择&#x200B;_跳出率_。
1. 将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为`by month`。
1. 为您的报告提供一个名称（如`Bounce rate by month`），然后单击&#x200B;**[!UICONTROL Save]**。

**现在，查看新访客与回访访客的平均会话时长：**

1. 创建报告。
1. 单击&#x200B;**UICONTROL添加量度**，将鼠标悬停在下拉列表底部的[!DNL Google Analytics]部分上并选择`Average Session Length`。
1. 是否将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为`by month`？
1. 添加`Group by`并选择`New or returning visitor`。  选中`Show All`框；然后单击&#x200B;**[!UICONTROL Apply]**。
1. 为您的报告提供一个名称（如`Average session length`），然后单击&#x200B;**[!UICONTROL Save]**。

**接下来，查看过去30天内排名最前的反向链接域：**

1. 创建报告。
1. 单击&#x200B;**[!UICONTROL Add Metric]**，将鼠标悬停在下拉列表底部的[!DNL Google Analytics]部分上并选择`Sessions`。
1. 将您的时间段更改为从31天前到1天前的移动范围，并将时间间隔调整为`none`。
1. 添加`Group by`并选择`ga:source`。  选中&#x200B;_显示全部_&#x200B;框；然后单击&#x200B;**[!UICONTROL Apply]**。
1. 添加其他`group by`并选择`ga:medium`。 再次选中`Show All`框；然后单击&#x200B;**[!UICONTROL Apply]**。
1. 为您的报告提供一个名称（如`Top 20 Referring Domains, 30 Days`），然后单击&#x200B;**[!UICONTROL Save]**。

**最后，查看转换：**

1. 创建报告。
1. 添加以下量度：

* `New users`
   * 单击量度名称下方的&#x200B;**[!UICONTROL Hide]**

* `Number of orders`
   * 为`Customer's order number` = 1添加筛选器并单击&#x200B;**[!UICONTROL Apply]**
   * 通过单击量度名称，将其命名为`Number of first orders`，然后单击&#x200B;**[!UICONTROL Hide]**&#x200B;来重命名该量度

* `Number of orders`
   * **[!UICONTROL Hide]**&#x200B;指标

* `Users`
   * **[!UICONTROL Hide]**&#x200B;指标
   * 将时间段更改为`24 months ago to now`，并将时间间隔调整为`by month`。
   * 通过单击&#x200B;**[!UICONTROL Formula]**&#x200B;添加以下公式。
   * A/D，然后单击&#x200B;**[!UICONTROL Apply]**
   * 重命名公式`Registration conversion`
   * B/D ，然后单击&#x200B;**[!UICONTROL Apply]**
   * 重命名公式`First order conversion`
   * C/D，然后单击&#x200B;**[!UICONTROL Apply]**
   * 重命名公式`Any order conversion`

* 现在，为您的报表提供一个名称，如`Conversion by month`，然后单击&#x200B;**[!UICONTROL Save]**。

## 后续步骤

现在，您可以访问有关网站流量和转化率的数据，接下来可以开始挖掘这些数据以做出业务决策，例如，哪些网站最能提升您网站的流量？ 或您的哪些营销活动在吸引具有高存留期价值的客户方面最有效？

在调整广告支出和营销策略时，您可以继续跟踪[!DNL Commerce Intelligence]中的结果，在此信息板上反复迭代，以满足贵公司不断变化的优先级。
