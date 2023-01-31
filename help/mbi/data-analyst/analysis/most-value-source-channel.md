---
title: 确定最有价值的营销来源和渠道
description: 了解一些可用于发现最有价值的营销渠道的报表。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# 确定成功的营销源

您研究了受众，创建了营销活动，投资了一些营销渠道。 现在已经过了一段时间了，这些渠道的表现如何？ 哪些渠道引入了最新用户？ 哪个来源对您的总收入贡献最大？

使用 [!DNL MBI]，则可以按反向链接来源轻松划分收入和用户，而无论该来源是否与 [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) 或自定义数据字段。 利用此分段，可找到性能最佳的渠道，并更好地投入营销预算。

在本文中，我们将探索一些可用于发现最有价值的营销渠道的报表：

* [按来源划分的新用户](#newusersbysource)
* [按用户来源划分的平均生命周期收入](#avglifetimerev)
* [按用户来源划分的平均订单值](#avgorderval)
* [按用户注册日期和来源列出的收入](#revbyregdateandsource)
* [按用户来源重复订单](#repeatordersbysource)

## 先决条件 {#prereqs}

要构建本文中的分析，您需要访问营销客户获取/反向链接源数据。 如果您尚未跟踪它，则需要将 [订单反向链接源数据 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL MBI] 才能继续。 此外，向分析添加用户设备信息使您能够查看推荐使用的技术。

## 按来源划分的新用户 {#newusersbysource}

评估推荐来源的性能是确定您最有价值渠道的关键。 此报表按客户获取来源显示一段时间内新注册用户的数量，从而允许您跟踪反向链接来源在获取新注册用户时的性能。

要在 [Report Builder](../../tutorials/using-visual-report-builder.md)，添加 **新用户** 量度（或计算一段时间内新用户数量的等效量度）。 然后，执行以下操作：

1. 设置 [!UICONTROL Time Period] 到要分析的注册期。
1. 设置 [!UICONTROL Interval] 每月。
1. 已设置 [!UICONTROL Group By] 要获取（或反向链接）来源，请选择要包含的来源。
1. 在本例中，我们使用 `stacked columns` [!UICONTROL chart type].

下面是一个直观的演示：

![按源创建新用户报表。](../../assets/New_Users_by_source.gif)

## 按用户来源划分的平均生命周期收入 {#avglifetimerev}

找到吸引新用户的渠道非常重要，但这些引荐的总体价值如何？ 此报表显示特定客户获取来源用户在一段时间内的平均生命周期收入。 换句话说，这允许您查看从特定来源获得的用户在其生命周期中是否与从其他来源获得的一组用户相比花费更多。

要在Report Builder中创建此报表，请将 **平均存留期收入** 量度。 然后，执行以下操作：

1. 设置 [!UICONTROL Time Period] 到要分析的时间段。
1. 设置 [!UICONTROL Interval] 每月。
   [!UICONTROL Group By] 要获取（或反向链接）来源，请选择要包含的来源。
1. 在本例中，我们使用 `line chart` 类型。

以下是一个可视化演练：

![按用户源创建平均生命周期收入](../../assets/Lifetime_revenue_by_user_source.gif).

此示例仅查看生命周期收入，但您也可以复制此分析以查看 [!UICONTROL Number of orders] 或 [!UICONTROL Distinct buyers] 推荐。

## 按用户来源划分的平均订单值 {#avgorderval}

为了更好地了解用户从特定客户获取源中花费的金钱，您可以构建一个报告来查看其平均订单值。 这样，您就可以跟踪从特定来源获取的用户每次订购支出是否多于从其他来源获取的用户。

要在Report Builder中创建此报表，请将 **平均订单值** 量度，然后执行以下操作：

1. 设置 [!UICONTROL Time Period] 到要分析的注册期。
1. 设置 [!UICONTROL Time Interval] 每月。
1. 已设置 [!UICONTROL Group By] 要获取（或反向链接）来源，请选择要包含的来源。
1. 在本例中，我们使用 **堆叠列** 图表类型。

以下是一个可视化演练：

![按用户来源创建平均订单值报表。](../../assets/Average_order_value_by_source.gif)

## 按用户注册日期和来源列出的总收入 {#revbyregdateandsource}

我们前面介绍的生命周期收入分析允许您查看从不同来源获得的用户的平均生命周期收入，但是，总生命周期收入呢？ 利用此报表，可确定在特定时间内注册的特定来源用户所产生的总体收入。

要在Report Builder中创建此报表，请将 `Revenue by user registration date` 量度。 如果您没有 [创建此量度](../../data-user/reports/ess-manage-data-metrics.md) 你可以通过复制 `Revenue` 量度和更改 `time stamp` 到用户的 `creation date`. 添加量度后，请执行以下操作：

1. 设置 [!UICONTROL Time Period] 到要分析的注册期。
1. 设置 [!UICONTROL Time Interval] 每月。
1. 已设置 [!UICONTROL Group By] 要获取（或反向链接）来源，请选择要包含的来源。
1. 在本例中，我们使用 `stacked columns` 图表类型。

以下是一个可视化演练：

![创建按用户注册日期和来源列出的总收入报表。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 按用户来源重复订单 {#repeatordersbysource}

“平均订单值”报表显示用户在下订单时从特定来源获得的平均支出。 但是，此报表不会显示这些用户是否是重复客户。 但是，通过按用户源重复订单，您可以查看特定来源的用户是否进行了更多或更少的重复购买。

要在 [Report Builder](../../tutorials/using-visual-report-builder.md)，添加 **订单数** 量度，然后执行以下操作：

1. 设置 [!UICONTROL Time Period] 到要分析的注册期。
1. 设置 [!UICONTROL Time Interval] 每月。
1. 添加 [!UICONTROL filter] 以便仅包含具有重复订单的用户：

   用户的订单号大于1

1. 已设置 [!UICONTROL Group By] 要获取（或反向链接）来源，请选择要包含的来源。
1. 在本例中，我们使用 `stacked columns` 图表类型。

以下是一个可视化演练：

![按用户来源创建重复订单报表。](../../assets/Repeat_orders_by_user_source.gif)


## 包装 {#wrapup}

在本文中，我们仅介绍了可用于分析您的收购和营销渠道价值的一些分析，但这只是冰山一角。 如果您创建了我们未在此处涵盖的强大分析，请让我们了解您在评论中所执行的操作。

## 相关 {#related}

* [通过跟踪订单反向链接源 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [连接 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [建筑 [!DNL Google ECommerce] 包含订单和客户数据的维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [中UTM标记的最佳实践 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
