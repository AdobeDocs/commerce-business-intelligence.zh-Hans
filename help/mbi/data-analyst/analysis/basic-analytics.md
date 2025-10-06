---
title: 了解和构建基本分析
description: 了解如何了解和构建基础分析。
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Dashboards, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '3130'
ht-degree: 0%

---

# 基本Analytics

在您熟悉[!DNL Adobe Commerce Intelligence]平台并基本了解该工具后，您将需要开始构建报告。 您可能遇到的一个最常见问题是“我应该查看什么？”

以下信息概述了一些您可能会认为有价值的常见量度和报表。 这些报表中的某些报表存在于您的帐户中，因此请确保查看存在于您帐户中的量度和报表，以避免创建重复项。

## 要了解的表和列

构建量度时，您需要了解四项信息：

1. 数据所在的那张表，
1. 要执行的特定操作，
1. 要对其执行该操作的列，以及
1. 要用于跟踪该数据的时间戳。

这些示例中使用的表的名称很可能与数据库中的列名和表名略有不同，因为每个数据库都是唯一的。 如果您需要帮助来标识数据库中的相应表或列，请引用以下定义。

## Customers表

此表包含有关每个客户的关键信息，如唯一的客户ID、电子邮件地址等。 以下示例使用&#x200B;**[!UICONTROL customer_entity]**&#x200B;作为示例客户表的名称。

如果某些计算当前不存在于您的数据库中，则您帐户中的任何管理员用户都可以生成这些计算。 此外，您还希望确保这些维度可分组到所有适用的量度。

**维度**

* **[!UICONTROL Entity_id]**：每个客户的唯一标识符。 这也可能是唯一的客户编号或客户电子邮件地址，它应该用作订单表的参考键。
* **[!UICONTROL Created_at]**：创建客户帐户并将其添加到数据库的日期。
* **[!UICONTROL Customer's lifetime revenue]**：客户产生的总生命周期收入。
* **[!UICONTROL Customer's first 30-day revenue]**：客户在前30天内产生的收入总额。
* **[!UICONTROL Customer's lifetime number of orders]**：客户在其生命周期内下达的订单数。
* **[!UICONTROL Customer's lifetime number of coupons]**：客户在其存留期内使用的优惠券总数。
* **[!UICONTROL Customer's first order date]**：客户第一张订单的日期。 这可能与created_at日期不同，如果客户在创建时没有下订单。

**您接受来宾订单吗？**

*如果是，此表可能不包含您的所有客户。 请联系[支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以确保您的客户分析包括所有客户。*

*不确定您是否接受来宾订单？ 请参阅[此主题](../data-warehouse-mgr/guest-orders.md)以了解详情！*

## 订单表

在此表中，每一行代表一个顺序。 此表中的列包含有关每个订单的基本信息，如订单的ID、创建日期、状态、下订单的客户的ID等等。 以下示例使用&#x200B;**[!UICONTROL sales_flat_order]**&#x200B;作为示例订单表的名称。

**维度**

* **[!UICONTROL Customer_id]**：下订单的客户的唯一标识符。 这通常用于在customer表和orders表之间移动信息。 在这些示例中，**[!UICONTROL sales_flat_order]**&#x200B;表上的customer_id应与&#x200B;**[!UICONTROL entitiy_id]**&#x200B;表上的&#x200B;**[!UICONTROL customer_entity]**&#x200B;一致。
* **[!UICONTROL Created_at]**：创建或下订单的日期。
* **[!UICONTROL Customer_email]**：下订单的客户的电子邮件地址。 这也可能是客户的唯一标识符。
* **[!UICONTROL Customer's lifetime number of orders]**： `Customers`表中同名列的副本。
* **[!UICONTROL Customer's order number]**：与订单关联的客户连续订单号。 例如，如果您正在查看的行是客户的第一张订单，则此列为“1”；但是，如果这是客户的第十五张订单，则此列显示此订单的“15”。 如果`Customers`表上不存在此维度，请联系[支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)来帮助您构建它。
* **[!UICONTROL Customer's order number (previous-current)]**： **[!UICONTROL Customer's order number]**&#x200B;列中两个值的连接。 它用在下面的示例报表中，以显示任意两张订单之间经过的时间。 例如，客户第一次订购日期与第二次订购日期之间的时间在此计算中表示为“1-2”。
* **[!UICONTROL Coupon_code]**：显示每个订单使用了哪些优惠券。
* **[!UICONTROL Seconds since previous order]**：客户订单之间的时间（以秒为单位）。

## 订单项目表

在此表中，每一行表示售出的一件商品。 此表包含有关每个订单中销售物料的信息，如订单参考编号、产品编号、数量等。 以下示例使用`sales_flat_order_item`作为示例订单项表的名称。

**维度**

* **[!UICONTROL Item_id]**：表中每一行的唯一标识符。
* **[!UICONTROL Order_id]**： `Orders`表的引用键，它告诉您哪些项目是同一订单购买的。 如果订单包含多个项目，则重复该值。
* **[!UICONTROL Product_id]**：如果您需要有关所购买的特定产品的信息（如颜色、大小等），可使用此列从产品表中提取该信息。
* **[!UICONTROL Order's created_at]**：下订单的时间戳，通常从`order line items`表中复制到`Orders`表中。
* **[!UICONTROL Order's coupon_code]**：与`Order's created_at`维度类似，此列是从您的订单表中复制的。

## “预订”表

此表用于管理您的订阅信息，如订阅ID、订阅者的电子邮件地址、订阅开始日期等。

**维度**

* **[!UICONTROL Customer_id]**：下订单的客户的唯一标识符。 这是在Customers表和Orders表之间建立路径的常用方法。 在这些示例中，**sales_flat_order**&#x200B;表上的customer_id应与`entitiy_id`表上的`customer_entity`一致。
* **[!UICONTROL Start date]**：客户开始订阅的日期。

## 营销支出表

在分析营销支出时，您可以在分析中包含[!DNL Facebook]、[!DNL Google AdWords]或其他来源。 如果您有多个营销支出来源，请联系[Managed Services团队](https://business.adobe.com/products/magento/fully-managed-service.html)，以获取有关为您的营销活动设置合并表的帮助。

**维度**

* **[!UICONTROL Spend]**：广告总支出。 在[!DNL Facebook]中，这将是`facebook_ads_insights_####`表中的支出列。 对于[!DNL Google AdWords]，这将是`adCost`表中的`campaigns####`列。
* 附加到每个表的`####`与[!DNL Facebook]或[!DNL Google AdWords]帐户的特定帐户ID相关。
* **[!UICONTROL Clicks]**：点击总数。 在[!DNL Facebook]中，这将是`facebook_ads_insights_####`表中的点击数列。 在[!DNL Google AdWords]中，这将是`campaigns####`表中的adClicks列。
* **[!UICONTROL Impressions]**：展示总数。 在[!DNL Facebook]中，这就是`facebook_ads_insights_####`表中的展示次数。 在[!DNL Google AdWords]中，这就是`campaigns####`表的展示次数。
* **[!UICONTROL Campaign]**：点击总数。 在[!DNL Facebook]中，这将是`facebook_ads_insights_####`表中的campaign_name列。 在[!DNL Google AdWords]中，这将是`campaigns####`表中的促销活动列。
* **[!UICONTROL Date]**：针对特定营销活动发生的活动（支出、点击次数或展示次数）的时间和日期。 在[!DNL Facebook]中，这将是`date_start`表中的`facebook_ads_insights_####`列。 在[!DNL Google AdWords]中，这将是`campaigns####`表中的日期列。
* **[!UICONTROL Customer's first order's source]**：来自客户第一张订单的订单来源。 首先，检查您的帐户中是否有名为`customer's first order's source`的列。 如果您没有看到此列，则可以使用这些说明创建所需的列。
* **[!UICONTROL Customer's first order's medium]**：来自客户第一张订单的订单媒介。 首先，检查您的帐户中是否有名为`customer's first order's source`的列。 如果您没有看到此列，则可以使用这些说明创建所需的列。
* **[!UICONTROL Customer's first order's campaign]**：客户的第一个订单中的订单促销活动。 首先，检查您的帐户中是否有名为`customer's first order's source`的列。 如果您没有看到此列，则可以使用这些说明创建所需的列。

## 常见报表和量度

以下是您可能会觉得有用的报表和量度的一些常见示例：

* [Customer Analytics](#customeranalytics)
* [Order Analytics](#orderanalytics)
* [营销支出分析](#mktgspendanalytics)

## 客户分析 {#customeranalytics}

### 新用户

* **描述**：给定时间段内新获得的用户的总数。 `New Users`与`Unique Customers`不同，因为`New Users`具有使用您的服务创建帐户的时间戳（这并不意味着他们一定已下订单），而`Unique Customers`已至少下过一次订单。
* **量度定义**：此量度执行从&#x200B;**排序的**&#x200B;表中进行的`entity_id`计数`customer_entity`（共`created_at`个）。
* **报告示例**：上个月创建的新用户数
   * **[!UICONTROL Metric]**： `New Users`
   * **[!UICONTROL Time Range]**： `Last Month`
   * **[!UICONTROL Time Interval]**： `By Day`

![新用户](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### 独特客户

* **描述**：给定时段内不同客户的总数。 这与`New Users`不同，因为它仅跟踪至少下过一次订单的客户。 独特客户报表在给定时间间隔内仅跟踪客户一次。 如果将时间间隔设置为`By Day`，并且客户当天进行了多次购买，则客户将只被计数一次。 如果您要查看购买的总数，请查看`Number of Orders`。
* **量度定义**：此量度执行&#x200B;**排序的**&#x200B;表中`customer_id`的`sales_flat_order`非重复计数`created_at`。
* **报告示例**：过去90天内按周划分的不同客户
   * **[!UICONTROL Metric]**： `Distinct Customers`
   * **[!UICONTROL Time Range]**： `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**： `By Day`

![独特客户。](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### 新订阅者

* **描述**：在给定期间内获得的新订阅者的总数。
* **量度定义**：此量度执行&#x200B;**排序的**&#x200B;表中`customer_id`的`subscriptions`非重复计数`start_date`。
* **报告示例**：按月列出今年的新订阅者
   * **[!UICONTROL Metric]**： `New Subscribers`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**： `By Month`

![个订阅者](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### 回头客

* **描述**：在某个时段内下多张订单的客户总数。 在重复客户报表中，您可以使用`Distinct Customers`表中的`Customer's Order Number`量度和`orders`维度。
* **使用的量度**： `Distinct Customers`
* **报告示例**：去年第2次和第3次购买的次数
   * **[!UICONTROL Metric]**： `Distinct Customers`
   * **[!UICONTROL Time Range]**： `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**： `By Month`
   * **[!UICONTROL Group By]**： `Customer's Order Number`，然后选择`2`和`3`

  ![显示去年第二和第三次购买分析的图表](../../assets/2nd_and_3rd_purchases_last_year.png)

* **报告示例2**：去年的重复客户数量
   * **[!UICONTROL Metric]**： `Distinct Customers`
   * **[!UICONTROL Filters]**： `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**： `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**： `By Month`

  ![去年回头客](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### 按生命周期订单数排列的顶级客户

* **描述**：基于订单总数的顶级客户列表。 这会为您提供最频繁购物者的直接列表。
* **使用的量度**： `Orders`
* **报告示例**：按生命周期订单数排在前25位的客户
   * **[!UICONTROL Metric]**： `Orders`
   * **[!UICONTROL Time Range]**： `All Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**： `customer_email`
   * **[!UICONTROL Show Top/Bottom]**：按订单排序的前25项

  ![前25位客户（按订单）](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### 按生命周期收入排列的顶级客户

* **描述**：基于生命周期收入的顶级客户列表。
* **使用的量度**： `Average Lifetime Revenue`
* **报告示例**：按生命周期收入排在前25位的客户
   * **[!UICONTROL Metric]**： `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**： `All time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**： `customer_email`
   * **[!UICONTROL Show Top Bottom]**：按生命周期收入排序的前25个

  ![按收入排列的前25位客户](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### 按同类群组列出的平均生命周期收入

* **描述**：跟踪一段时间内不同同类群组[用户的](../dev-reports/lifetime-rev-cohort-analysis.md)平均生命周期收入，以确定表现最佳的同类群组。 同类群组按通用日期（如首次订购日期或创建日期）分组。
* **使用的量度**： `Revenue`
* **报告示例**：按同类群组划分的平均客户存留期收入
   * **[!UICONTROL Metric]**： `Revenue`
   * **[!UICONTROL Cohort Date]**： `Customer's first order date`
   * **[!UICONTROL Time Interval]**： `Month`
   * **[!UICONTROL Time Period]**：移动最近八个同类群组中的一组同类群组，其中至少有四个月的数据
   * **[!UICONTROL Duration]**： `12 Month(s)`
   * **[!UICONTROL Table]**： `Customer_entity`
   * **[!UICONTROL Perspective]**：每个同类群组成员的累积平均值

  ![同类群组的客户存留期收入](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### 按优惠券使用情况划分客户

* **描述**：已获取且使用优惠券/折扣代码的客户的计数。 这有助于您清楚地了解折扣寻求者与全价购买者的情况。
* **使用的量度**： `New Users`
* **报告示例**：按月显示优惠券和非优惠券客户
   * **[!UICONTROL Metric A]**： `Non coupon customers`
   * **[!UICONTROL Metric]**： `New Users`
   * **[!UICONTROL Filters]**：客户存留期订单数大于0且客户存留期优惠券数等于0
   * **[!UICONTROL Metric B]**： `Coupon customers`
   * **[!UICONTROL Metric]**： `New Users`
   * **[!UICONTROL Filters]**：客户存留期订单数大于0且客户存留期优惠券数大于0
   * **[!UICONTROL Time range]**： `All Time`
   * **[!UICONTROL Time interval]**： `By Month`

  ![客户（按优惠券使用情况）](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **报告示例2**：按月的优惠券和非优惠券客户的百分比
   * **[!UICONTROL Metric A]**： `Non coupon customers` （隐藏量度）
      * **[!UICONTROL Metric]**： `New Users`
      * **[!UICONTROL Filters]**： `Customer's Lifetime Number of Orders Greater Than 0`和`Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**： `Coupon customers`
      * **[!UICONTROL Metric]**： `New Users`
      * **[!UICONTROL Filters]**： `Customers Lifetime Number of Orders Greater Than 0`和`Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**： `All Time`
   * **[!UICONTROL Time Interval]**： `By Month`
   * **[!UICONTROL Formula]**： `B/(A+B)`

>[!NOTE]
>
> **隐藏所有量度**

![优惠券使用量](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### 平均前30天收入

* **描述**：客户在作为客户的前30天内产生的平均收入额。
* **量度描述**：此量度执行从&#x200B;**表中按**&#x200B;排序的`Customer's First 30 Day Revenue`平均`customer_entity`（共`created_at`个）。
* **报表描述**：客户前30天收入的所有时间平均值
   * **[!UICONTROL Metric]**： `Average First 30 Day Revenue`
   * **[!UICONTROL Time Range]**： `All Time`
   * **[!UICONTROL Time Interval]**： `None`

![平均前30天收入](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### 平均客户存留期收入

* **描述**：客户在其生命周期内生成的平均收入额。
* **量度描述**：此量度在基于&#x200B;**的**&#x200B;表上执行`Customer's Lifetime Revenue`列的`customer_entity`平均`created_at`。
* **报表描述**：客户生命周期收入的所有时间平均值
   * **[!UICONTROL Metric]**： `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**： `All Time`
   * **[!UICONTROL Time Interval]**： `None`

![客户存留期收入](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## 订单分析 {#orderanalytics}

### 收入

* **描述**：收入量度显示选定时间段内获得的收入总计。
* 此量度执行&#x200B;**表中按**&#x200B;排序的`grand_total`总和`sales_flat_order`（共`created_at`个）。
* **报告示例**：按月份、年累计的收入
   * **[!UICONTROL Metric]**： `Revenue`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 1 Month Ago`
   * **时间间隔**： `By Month`

>[!TIP]
>
>确保您的收入量度的计算与您内部讨论的定义保持一致。 例如，您可能需要对已发运的订单收入进行计数、折换不同区域的币种或排除税。 此外，您可以使用[筛选器集](../../data-user/reports/ess-manage-data-filters.md)来确保基于同一表生成的所有量度的一致性。

![收入](../../assets/revenue.png)<!--{: width="929"}-->

### 订购

* **描述**：给定时段内订单总数的计数。 订单报表跟踪因新产品供应、促销或任何其他可能增加（或减少）交易量而对订单量所做的更改。 您可能经常希望按某些变量划分此量度以回答您的问题。
* **量度定义**：此量度执行&#x200B;**排序的**&#x200B;表中`entity_id`的`sales_flat_order`计数`created_at`。
* **报告示例**：按月份、年累计的订单
   * **[!UICONTROL Metric]**： `number of orders`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**： `By Month`

>[!TIP]
>
>与收入量度一样，您应该实施[过滤器集](../../data-user/reports/ess-manage-data-filters.md)以排除不完整、测试或返回的订单。

![订单](../../assets/orders_pic.png)<!--{: width="929"}-->

### 订购的产品

* **描述**：订购的产品量度可告知您特定时间段内售出的商品数量。
* **量度定义**：此量度执行&#x200B;**排序的**&#x200B;表中`qty_ordered`的`sales_flat_order_item`总和`created_at`。
* **报告示例**：按月份、按年度列出的销售项目
   * **[!UICONTROL Metric]**： `Products ordered`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**： `By Month`

  已订购![个产品](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* 将此量度与您的订单数量度组合，以计算每订单的项目数。 接下来，将优惠券代码添加到报表中，以确定您的促销活动对购物车大小有何影响，或按新订单与重复订单进行分段，从而更好地了解您的客户行为。
* **报告示例**：每订单产品：第一订单与重复订单
   * **[!UICONTROL Metric A]**：已订购的产品：第一笔订单
      * **[!UICONTROL Metric]**： `Products ordered`
      * **[!UICONTROL Filter]**： `Customer's order number = 1`
   * **[!UICONTROL Metric B]**：订单：第一笔订单
      * **[!UICONTROL Metric]**： `Orders`
      * **[!UICONTROL Filter]**： `Customer's order number = 1`
   * **[!UICONTROL Metric C]**：已订购的产品：重复订购
      * **[!UICONTROL Metric]**： `Products ordered`
      * **[!UICONTROL Filter]**： `Customer's order number > 1`
   * **[!UICONTROL Metric D]**：订单：重复订单
      * **[!UICONTROL Metric]**： `Orders`
      * **[!UICONTROL Filter]**： `Customer's order number > 1`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**： `By Week`
   * **[!UICONTROL Formula 1]**： `A/B`
   * **[!UICONTROL Formula 2]**： `C/D`

>[!NOTE]
>
>取消选中`Multiple Y-Axes box`和`Hide`所有指标

![订购的产品2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### 平均订单值

* **描述**：跟踪一段时间内所下订单的平均值。 使用此量度可快速确定平均订单价值(AOV)因营销工作、产品和/或业务中的其他变化而出现波动的情况。
* **量度定义**：此量度从按&#x200B;**排序的**&#x200B;表中执行`grand_total`平均`sales_flat_order`（共`created_at`个）。
* **报告示例**： AOV与上一年，YTD
   * **[!UICONTROL Metric]**： `Average order value`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**： `By Month`
   * **[!UICONTROL Perspective]**： `Amount Change vs Previous Year`

  ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### 购买次数最多的产品（含优惠券）

* **描述**：此报表可提供insight在您提供促销或优惠券时将销售哪些产品。
* **使用的量度**：订购的产品
* **报告示例**：使用优惠券购买次数最多的产品
   * **[!UICONTROL Metric]**： `Products ordered`
   * **[!UICONTROL Filter]**： `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By**]： `name`（或`SKU`，或任何其他产品标识符）
   * **[!UICONTROL Show top/bottom]**：按订购的产品排在前25位

  ![带优惠券的产品](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### 订单之间的时间

* **描述**：测试您对客户购买周期的假设和预期，在订单之间使用&#x200B;**时间**&#x200B;分析，该分析查看购买之间的平均时间（或中间值！）。 在下图中，您可以看到您的最佳客户（下超过3份订单的客户）在不到六个月的时间内完成第二次购买。 未下第四张订单的客户需等待14个月再进行第二次购买。
* **量度定义**：此量度执行&#x200B;**排序的**&#x200B;中的`Time since previous order`平均`sales_flat_order`次（共`created_at`次）。
* **报告示例**：
   * **量度1**：≤3个订单
      * **[!UICONTROL Metric]**： `Average time between orders`
      * **[!UICONTROL Filter]**： `Customer's lifetime number of orders ≤ 3`
   * **指标2**： > 3个订单
      * **[!UICONTROL Metric]**： `Average time between orders`
      * **[!UICONTROL Filter]**： `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**：` Customer's order number (previous-current)`

>[!NOTE]
>
>取消选中`Multiple Y-Axes`框。

订单之间的![时间](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## 营销支出分析 {#mktgspendanalytics}

### 广告支出

* **描述**：您可以按促销活动、广告集或其他分段，分析不同时间段和间隔内的营销支出。
* **量度定义**：此量度对`Marketing Spend`表中按`date`列排序的支出列执行总和。
* **报告示例**：按促销活动划分的广告支出
   * **[!UICONTROL Metric]**： `Ad spend`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**： `campaign`

![广告支出](../../assets/ad_spend.png)<!--{: width="929"}-->

### 广告展示次数和广告点击次数

* **描述**：除了分析广告支出之外，您还可以分析广告展示次数和广告点击次数。
* **量度定义**：此量度对`Marketing Spend`表中按日期列排序的展示次数（或点击次数）列执行总和。
* **报告示例**：按日期添加展示次数和广告点击次数
   * **[!UICONTROL Metric A]**： `Ad impressions`
   * **[!UICONTROL Metric B]**： `Ad clicks`
   * **[!UICONTROL Time Range]**： `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**： `By Day`

  ![广告展示次数](../../assets/ad_impressions.png)<!--{: width="929"}-->

### 点进率(CTR)

* **描述**：使用上面创建的广告展示次数和广告点击量量度，您可以按不同促销活动在一段时间内分析您的点进率。
* **报告示例**：按营销活动列出的CTR
   * **[!UICONTROL Metric A]**： `Ad impressions`
   * **[!UICONTROL Metric B]**： `Ad clicks`
   * **[!UICONTROL Time Range]**：`All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Formula]**： `B/A`
   * 选择`%`选项。
   * **[!UICONTROL Group By]**： `campaign`

>[!NOTE]
>
>您可以&#x200B;**标题**&#x200B;公式为`CTR`，并&#x200B;**隐藏**&#x200B;所有指标。

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### 每次点击成本(CPC)

* **描述**：使用上面创建的广告支出和广告点击量指标，您可以按不同促销活动分析一段时间内的每次点击成本。
* **报告示例**：按营销活动列出的CPC
   * **[!UICONTROL Metric A]**： `Ad spend`
   * **[!UICONTROL Metric B]**： `Ad clicks`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Formula]**： `A/B`
   * 选择`currency`选项
   * **[!UICONTROL Group By]**： `campaign`

>[!NOTE]
>
>您可以&#x200B;**标题**&#x200B;公式为`CPC`，并&#x200B;**隐藏**&#x200B;所有指标。

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### 按客户获取来源列出的客户

* **描述**：如果您使用[!DNL Google eCommerce]跟踪订单的来源、媒介和促销活动，则可以按客户获取来源分析客户。 这有助于您识别哪些营销来源正在获取客户，并回答诸如“您的大多数客户是否通过[!DNL Google]、[!DNL Facebook]或某个其他来源发出第一笔订单？”
* **报表示例**：按客户获取源列出的客户
   * **[!UICONTROL Metric Used]**： `New Customers`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `By Month`
   * **[!UICONTROL Group By]**： `Customer's first order's source`

>[!NOTE]
>
>查看[本文](../analysis/most-value-source-channel.md)，了解更多使用客户获取源的报表示例。

![客户获取Source](../../assets/acquisition_source.png)<!--{: width="929"}-->

### 按客户获取媒介和客户获取促销活动划分的客户

* **描述**：与按客户获取来源分析客户类似，您也可以按客户第一订单的媒体和促销活动分析客户。 这可以帮助您回答诸如“哪些营销活动在吸引新客户？”之类的问题。
* **报告示例**：按带付费媒体的客户获取促销活动列出的客户
   * **[!UICONTROL Metric Used]**： `New customers`
   * **[!UICONTROL Filter]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**： `Customer's first order's campaign`

>[!NOTE]
>
>对于`New Customers`量度中的筛选器，您可以为业务添加任何视为“付费”媒介的其他媒介，例如cpc或付费搜索。

![客户获取Medium](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### 客户购置成本(CAC)或每次购置成本(CPA)

* **描述**：分析促销活动成本的一种方法是，将所有成本仅归因于通过促销活动获得的客户。
* **报告示例**：按营销活动列出的CAC
   * **[!UICONTROL Metric A]**： `New customers`
   * **[!UICONTROL Filter]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**： `Ad Spend`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Formula]**： `B/A`
   * 选择`currency`选项
   * **[!UICONTROL Group By]**：
      * 对于量度`A`，选择`Customer's first order's campaign`
      * 对于量度`B`，选择`campaign`

  ![新用户。](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>您可以&#x200B;**标题**&#x200B;公式为`CTR`，并&#x200B;**隐藏**&#x200B;所有指标。 另外，请查看[此文章](../analysis/roi-ad-camp.md)以了解详细信息。

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### 按客户获取源、媒体和促销活动划分的生命周期值

* **描述**：除了分析每个促销活动获得的客户数量之外，您还可以分析这些客户的平均生命周期收入。 这有助于您识别：
   * 如果某些营销活动吸引大量客户，但这些客户的存留期值较低。
   * 如果某些促销活动吸引少量客户，但这些客户具有高存留期价值。
* **报告示例**：首先添加`New customers`量度。 然后，添加`Average lifetime revenue`量度。 选择所需的时间范围，然后选择`interval`作为`None`。 最后，选择`group by`选项作为`Customer's first order's campaign`。
   * **[!UICONTROL Metric A]**： `New Customers`
   * **[!UICONTROL Filter A]**： `Customer's first order's source`，如“%google%”
   * **[!UICONTROL Filter B]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**： `Average lifetime revenue`
   * **[!UICONTROL Filter A]**： `Customer's first order's source`，如“%google%”
   * **[!UICONTROL Filter B]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Group By]**： `Customer's first order's campaign`

>[!NOTE]
>
>对于这两个过滤器，您可以添加任何被视为您的业务“付费”媒介的其他媒介（例如cpc或付费搜索）。 您还可以添加任何其他要分析的源，如Facebook。 查看[本文](../analysis/roi-ad-camp.md)，了解有关CAC、LTV和ROI的更多详细信息。

按客户获取源、媒体和促销活动列出的![生命周期值](../../assets/LTV_2.png)<!--{: width="929"}-->

### 投资回报率(ROI)

* **描述**：按营销活动计算ROI的一种方法是分析通过营销活动下达的所有订单。 但是，另一种方法是分析通过营销活动获得的客户的生命周期值。 要分析ROI，请务必确保支出数据和事务型数据中的促销活动名称保持一致。 如果您创建以下报告，并且由于促销活动名称不匹配而没有ROI值，则可能需要查看已实施的[UTM标记](../../best-practices/utm-tagging-google.md)。
* **报告示例**：按营销活动列出的ROI
   * **[!UICONTROL Metric A]**： `New Customers`
   * **[!UICONTROL Filter A]**： `Customer's first order's source`，如“%google%”
   * **[!UICONTROL Filter B]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**： `Average lifetime revenue`
   * **[!UICONTROL Filter A]**： `Customer's first order's source`，如“%google%”
   * **[!UICONTROL Filter B]**： `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**： `Ad spend`
   * **[!UICONTROL Time Range]**： `All-Time`
   * **[!UICONTROL Time Interval]**： `None`
   * **[!UICONTROL Formula]**： `(B-(C/A))/(C/A)`
   * 选择`% `选项
   * **[!UICONTROL Group By]**：
      * 对于量度`A`和`B`，选择`Customer's first order's campaign`
      * 对于量度`C`，选择`campaign`

>[!NOTE]
>
>您可以将公式命名为“ROI”，并隐藏所有量度。 此外，您还可以调整量度中的过滤器以分析替代源和媒介。 此外，查看[此主题](../analysis/roi-ad-camp.md)，了解有关CAC、LTV和ROI的更多详细信息。

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
