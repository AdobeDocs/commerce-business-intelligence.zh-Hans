---
title: 确定最有价值的营销来源和渠道
description: 了解可用于发现您最有价值的营销渠道的一些报表。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# 确定成功的营销源

你调查了你的受众，你创建了你的营销活动，你投资了几个营销渠道。 一段时间已经过去了，这些渠道的效果如何？ 哪个渠道引入的新用户最多？ 哪个来源对您的总收入贡献最大？

使用[!DNL Adobe Commerce Intelligence]，您可以按反向链接来源轻松对您的收入和用户进行分段，无论该来源是对应于[[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en)还是自定义数据字段。 此分段允许您找到表现最佳的渠道并更好地投入营销预算。

本主题探究了可用于揭示您最有价值的营销渠道的一些报表：

* [按源的新用户](#newusersbysource)
* [按用户来源列出的平均生命周期收入](#avglifetimerev)
* [按用户来源的平均订单值](#avgorderval)
* [按用户注册日期和来源列出的收入](#revbyregdateandsource)
* [按用户来源重复订单](#repeatordersbysource)

## 先决条件 {#prereqs}

要构建本主题中的分析，您需要具有营销客户获取/反向链接源数据的访问权限。 如果您尚未跟踪它，则需要将[订单引用源数据从 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)引入[!DNL Adobe Commerce Intelligence]中，然后才能继续。 此外，将用户设备信息添加到分析中，使您能够查看反向链接使用的技术。

## 按源的新用户 {#newusersbysource}

评估反向链接来源的表现是确定最有价值渠道的关键。 此报告按客户获取来源显示一段时间内新注册用户的数量，从而允许您跟踪推荐来源在获取新注册用户方面的性能。

要在[Report Builder](../../tutorials/using-visual-report-builder.md)中创建此报表，请将&#x200B;**新用户**&#x200B;指标（或计算一段时间内新用户数的等效指标）添加到报表中。 然后执行以下操作：

1. 将[!UICONTROL Time Period]设置为要分析的注册期。
1. 将[!UICONTROL Interval]设置为每月。
1. 将[!UICONTROL Group By]设置为客户获取（或反向链接）源，并选择要包含的源。
1. 此示例使用`stacked columns` [!UICONTROL chart type]。

下面是可视化演练：

![正在按源报告创建新用户。](../../assets/New_Users_by_source.gif)

## 按用户来源列出的平均生命周期收入 {#avglifetimerev}

找到带来新用户的渠道很重要，但是这些反向链接总体价值如何？ 此报表可显示一段时间内来自特定客户获取来源的用户平均生命周期收入。 换言之，这允许您查看从特定来源获取的用户在其一生中与您的花费是否比从不同来源获取的一组用户多。

要在Report Builder中创建此报表，请将&#x200B;**平均生命周期收入**&#x200B;指标添加到报表中。 然后执行以下操作：

1. 将[!UICONTROL Time Period]设置为要分析的时间段。
1. 将[!UICONTROL Interval]设置为每月。
   [!UICONTROL Group By]到客户获取（或反向链接）源，然后选择要包含的源。
1. 此示例使用`line chart`类型。

下面是可视化演练：

![正在按用户源创建平均生命周期收入](../../assets/Lifetime_revenue_by_user_source.gif)。

此示例仅查看生命周期收入，但您也可以复制此分析以按反向链接来源查看[!UICONTROL Number of orders]或[!UICONTROL Distinct buyers]。

## 按用户来源的平均订单值 {#avgorderval}

要更好地了解用户从特定客户获取来源中花费了多少资金，您可以构建一份报告来查看其平均订单价值。 这样，您就可以跟踪从特定来源获取的用户在每一订单上的支出是否多于从其他来源获取的用户在每一订单上的支出。

要在Report Builder中创建此报表，请添加&#x200B;**平均订单值**&#x200B;指标，然后执行以下操作：

1. 将[!UICONTROL Time Period]设置为要分析的注册期。
1. 将[!UICONTROL Time Interval]设置为每月。
1. 将[!UICONTROL Group By]设置为客户获取（或反向链接）源，并选择要包含的源。
1. 此示例使用&#x200B;**栈叠列**&#x200B;图表类型。

下面是可视化演练：

![正在按用户来源创建平均订单值。](../../assets/Average_order_value_by_source.gif)

## 按用户注册日期和来源列出的总收入 {#revbyregdateandsource}

通过前面介绍的生命周期收入分析，您可以查看从不同来源获得的用户的平均生命周期收入，但是总生命周期收入呢？ 通过此报表，您可以确定在特定时间内注册并从特定来源产生的总收入用户数。

要在Report Builder中创建此报表，请添加`Revenue by user registration date`指标。 如果您尚未[创建此量度](../../data-user/reports/ess-manage-data-metrics.md)，可以通过复制`Revenue`量度并将`time stamp`更改为用户的`creation date`来执行此操作。 添加量度后，执行以下操作：

1. 将[!UICONTROL Time Period]设置为要分析的注册期。
1. 将[!UICONTROL Time Interval]设置为每月。
1. 将[!UICONTROL Group By]设置为客户获取（或反向链接）源，并选择要包含的源。
1. 此示例使用`stacked columns`图表类型。

下面是可视化演练：

![按用户注册日期和源报告创建总收入。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 按用户来源重复订单 {#repeatordersbysource}

平均订单值报表显示从特定来源获得的用户在下订单时的平均花费。 但是，此报表不显示这些相同的用户是否为回头客。 但是，通过按用户来源重复订购，您可以查看特定来源的用户是否重复购买。

要在[Report Builder](../../tutorials/using-visual-report-builder.md)中创建此报表，请添加&#x200B;**订单数**&#x200B;量度，然后执行以下操作：

1. 将[!UICONTROL Time Period]设置为要分析的注册期。
1. 将[!UICONTROL Time Interval]设置为每月。
1. 添加[!UICONTROL filter]，以便仅包含重复订购的用户：

   用户的订单号大于1

1. 将[!UICONTROL Group By]设置为客户获取（或反向链接）源，并选择要包含的源。
1. 此示例使用`stacked columns`图表类型。

下面是可视化演练：

![按用户来源创建重复订单报告。](../../assets/Repeat_orders_by_user_source.gif)


## 正在结束 {#wrapup}

本主题仅涉及可用于分析您的收购和营销渠道价值的几个分析，但这只是冰山一角。

## 相关 {#related}

* [通过 [!DNL Google ECommerce]跟踪订单反向链接来源](../importing-data/integrations/google-ecommerce.md)
* [正在连接您的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [使用订单和客户数据生成 [!DNL Google ECommerce] 维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [在 [!DNL Google Analytics]中进行UTM标记的最佳实践](../../best-practices/utm-tagging-google.md)
