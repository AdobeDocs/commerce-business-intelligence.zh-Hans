---
title: 分析网站活动和客户转化率
description: 了解如何设置一个功能板，用于跟踪您的网站活动（包括页面查看次数、会话数和用户）以及一段时间内您的客户转化率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 分析网站活动

[!DNL Adobe Commerce Intelligence] 使您可轻松地将广告成本数据与您的其余数据集成。 这不仅使您能够了解您的网站活动，而且使您能够推断网站上成为注册用户或进行购买的访客百分比。

本主题将演示如何设置一个功能板，用于跟踪您的网站活动（包括页面查看次数、会话数和用户）以及一段时间内客户的转化率。

## 先决条件

**导入您的广告成本数据**  — 连接 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) 到 [!DNL Adobe Commerce Intelligence]  — 这将自动同步 [!DNL AdWords] 在Commerce Intelligence方面的支出。

**跟踪用户获取渠道数据**  — 系上你的领带 [!DNL Google AdWords] 数据库中的特定订单的数据，您必须 [跟踪用户获取](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. 这允许您使用utm源和媒介连接每个订单。

## 用户获取促销活动

此报表的集合使用以下项目构建：

* 当您连接 [!DNL Google AdWords] 数据
* 您的帐户中应已可用的基本指标，例如 `Number of orders` 和 `New users`
* 加入时创建的Dimension [!DNL Google Analytics Ecommerce] 到数据库的数据，如订单的utm源和订单的utm介质。 如果您的帐户中当前没有这些字段，请联系支持团队

## 构建报告

**首先，创建一个显示一段时间内页面查看次数、会话数和用户数的报告：**

1. 创建报告。
1. 单击 **[!UICONTROL Add Metric]**，然后将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Page Views`.
1. 添加另一个量度，再次悬停在 [!DNL Google Analytics] 部分，这次选择 `Sessions`.
1. 添加第三个量度，再次将鼠标悬停在 [!DNL Google Analytics] 部分，这次选择 `Users`.
1. 现在，将您的时间段更改为从31天前到1天前的移动范围，并将时间间隔调整为 `by day`.
1. 为报表命名(例如， `Page views, sessions and users by day`)，然后单击 **[!UICONTROL Save]**.

**第二份报告考察了过去一年页面查看次数：**

1. 创建报告。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 _页面查看次数_.
1. 将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为 `by month`.
1. 为您的报表命名，如 `Page views by month,` 并单击 **[!UICONTROL Save]**.

**第三张图表审视了过去一年的反弹率：**

1. 创建报告。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 _跳出率_.
1. 将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为 `by month`.
1. 为您的报表命名，如 `Bounce rate by month`，然后单击 **[!UICONTROL Save]**.

**现在，查看新访客与回访访客的平均会话时长：**

1. 创建报告。
1. 单击 **UICONTROL添加量度**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Average Session Length`.
1. 将您的时间段更改为移动范围（从13个月前到1个月前），并将时间间隔调整为 `by month`？
1. 添加 `Group by` 并选择 `New or returning visitor`.  查看 `Show All` 框；然后单击 **[!UICONTROL Apply]**.
1. 为您的报表命名，如 `Average session length`，然后单击 **[!UICONTROL Save]**.

**接下来，查看过去30天内排名最前的反向链接域：**

1. 创建报告。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Sessions`.
1. 将您的时间段更改为从31天前到1天前的移动范围，并将时间间隔调整为 `none`.
1. 添加 `Group by` 并选择 `ga:source`.  查看 _全部显示_ 框；然后单击 **[!UICONTROL Apply]**.
1. 添加另一个 `group by` 并选择 `ga:medium`. 再次检查 `Show All` 框；然后单击 **[!UICONTROL Apply]**.
1. 为您的报表命名，如 `Top 20 Referring Domains, 30 Days`，然后单击 **[!UICONTROL Save]**.

**最后，查看转化：**

1. 创建报告。
1. 添加以下量度：

* `New users`
   * 单击 **[!UICONTROL Hide]** 在指标名称下

* `Number of orders`
   * 添加筛选条件 `Customer's order number` = 1并单击 **[!UICONTROL Apply]**
   * 通过单击指标名称并调用它来重命名指标 `Number of first orders`，然后单击 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 量度

* `Users`
   * **[!UICONTROL Hide]** 量度
   * 将时间段更改为 `24 months ago to now`，并将时间间隔调整为 `by month`.
   * 通过单击添加以下公式 **[!UICONTROL Formula]**.
   * A/D ，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `Registration conversion`
   * B/D ，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `First order conversion`
   * C/D ，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `Any order conversion`

* 现在为您的报告命名，例如 `Conversion by month`，然后单击 **[!UICONTROL Save]**.

## 后续步骤

现在您有权访问有关网站流量和转化率的数据，您可以开始挖掘这些数据以推动业务决策，例如，哪些网站最能推动流量流向您的网站？ 或者，您的哪些促销活动在吸引具有高存留期价值的客户方面最有效？

在调整广告支出和营销策略时，您可以继续跟踪以下各项的结果： [!DNL Commerce Intelligence]，在此功能板上进行迭代，以满足贵公司不断变化的优先级。
