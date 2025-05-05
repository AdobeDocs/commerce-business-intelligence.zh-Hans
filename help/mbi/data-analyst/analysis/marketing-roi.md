---
title: 营销ROI
description: 了解如何设置一个仪表板来跟踪您的渠道分析，包括汇总的ROI和按促销活动列出的分析。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 营销ROI

>[!NOTE]
>
>本主题包含有关使用原始架构和新架构的客户端的说明。 如果您在主工具栏中选择“管理数据”后有“Data Warehouse视图”部分可用，则您位于[新架构](../../administrator/account-management/new-architecture.md)。

如果您正在在线广告上花钱，则希望跟踪您的投资回报，并在进一步投资方面做出以数据为导向的决策。 本主题将演示如何设置一个功能板来跟踪您的渠道分析，包括汇总的ROI和按促销活动列出的分析。

![](../../assets/Marketing_dashboard_example.png)

在开始之前，您需要连接您的[[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md)、[[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md)和[[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md)帐户，并引入任何其他在线广告支出数据。 此分析包含[高级计算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 统一表

**原始架构：**&#x200B;若要汇总来自各种来源（如[!DNL Facebook Ads]或[!DNL Google Adwords]）的支出，Adobe建议创建所有广告支出的&#x200B;**整合表**。 您需要一名分析师为您完成此步骤。 如果您尚未这样做，请[提交主题为`[MARKETING ROI ANALYSIS]`的支持请求](../../guide-overview.md#Submitting-a-Support-Ticket)，分析人员将创建此表。

**新架构：**&#x200B;您可以按照[此分析库](../../data-analyst/data-warehouse-mgr/create-dw-views.md)主题中的示例进行操作。 在新体系结构中，统一表现在称为Data Warehouse视图。

## 计算列

要创建的列

* **`Consolidated Digital Ad Spend`**&#x200B;表
* **`Campaign name`**&#x200B;由Adobe分析师创建，作为&#x200B;**[MARKETING ROI ANALYSIS]**&#x200B;票证的一部分

**原始架构和新架构：**

* **`sales_flat_order`**&#x200B;表
   * **`Order's GA campaign`**
      * 选择定义： `Joined Column`
      * [!UICONTROL Create Path]：
      * &#x200B;

        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;

        [!UICONTROL One]: `ecommerce####.transaction_id`

      * 选择[!UICONTROL table]： `ecommerce####`
      * 选择[!UICONTROL column]： `campaign`
      * [!UICONTROL Path]： `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * 选择定义：联接列
      * 选择[!UICONTROL table]： `ecommerce####`
      * 选择[!UICONTROL column]： `medium`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce#####.transactionId

   * **`Order's GA source`**
      * 选择定义：联接列
      * 选择[!UICONTROL table]： `ecommerce####`
      * 选择[!UICONTROL column]： `source`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce#####.transactionId
^

* **`customer_entity`**&#x200B;表
* **`Customer's first order GA campaign`**
   * 选择定义： `Max`
   * 选择[!UICONTROL table]： `sales_flat_order`
   * 选择[!UICONTROL column]： `Order's GA campaign`
   * [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]：
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 选择定义： `Max`
   * 选择[!UICONTROL table]： `sales_flat_order`
   * 选择[!UICONTROL column]： `Order's GA source`
   * [!UICONTROL Path]： sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]：
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 选择定义： `Max`
   * 选择[!UICONTROL table]： `sales_flat_order`
   * 选择[!UICONTROL column]： `Order's GA medium`
   * [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]：
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`**&#x200B;表
* **`Customer's first order GA campaign`**
   * 选择定义： `Joined Column`
   * 选择[!UICONTROL table]： `customer_entity`
   * 选择[!UICONTROL column]： `Customer's first order GA campaign`
   * [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 选择定义：联接列
   * 选择[!UICONTROL table]： `customer_entity`
   * 选择[!UICONTROL column]： `Customer's first order GA source`
   * [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 选择定义： `Joined Column`
   * 选择[!UICONTROL table]： `customer_entity`
   * 选择[!UICONTROL column]： `Customer's first order GA medium`
   * [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`

## 量度

* **广告支出**
* 在&#x200B;**`Consolidated Digital Ad Spend`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`adCost`**&#x200B;列上
* 按&#x200B;**`date`**&#x200B;时间戳排序

* **广告展示次数**
* 在&#x200B;**`Consolidated Digital Ad Spend`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`Impressions`**&#x200B;列上
* 按&#x200B;**`Month`**&#x200B;时间戳排序

* **广告点击次数**
* 在&#x200B;**`Consolidated Digital Ad Spend`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`adClicks`**&#x200B;列上
* 按&#x200B;**`Month`**&#x200B;时间戳排序

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 报告

* **广告花费（所有时间）**
   * [!UICONTROL Metric]：广告支出

* 量度`A`：广告支出
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 间隔]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **广告客户获取（所有时间）**
   * [!UICONTROL Metric]： `New customers`
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

* 量度`A`： `Ad customer acquisitions`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 间隔]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **广告ROI**
   * [!UICONTROL Metric]：广告支出

   * [!UICONTROL Metric]： `New customers`
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

   * [!UICONTROL Metric]：平均生命周期收入
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

   * [!UICONTROL Formula]： `((C - (A / B)) / (A / B))`
   * &#x200B;

     [!UICONTROL Format]: `Percentage`

* 量度`A`： `Ad Spend (hide)`
* 量度`B`： `Ad customer acquisitions (hide)`
* 量度`C`： `Average LTV (hide)`
* [!UICONTROL Formula]： `Ads ROI`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 间隔]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **按Ga排列的订单数**
   * &#x200B;

     [!UICONTROL 量度]: `Orders`

* 量度`A`： `Orders`
* [!UICONTROL Time period]： `All time`
* [!UICONTROL Interval]： `By Month`
* [!UICONTROL Group by]： `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]: `Area`

* **按营销活动划分的广告ROI**
   * [!UICONTROL Metric]： `Ad Spend`

   * [!UICONTROL Metric]：`New customers`
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

   * [!UICONTROL Metric]：平均生命周期收入
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

   * [!UICONTROL Metric]：平均生命周期订单数
   * [!UICONTROL Filters]：
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： （[`A`]或[`B`]或[`C`]）和[`D`]

   * [!UICONTROL Formula]： `(A / B)`
   * &#x200B;

     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]： `(C - (A / B))`
   * &#x200B;

     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]： `((C - (A / B)) / (A / B))`
   * &#x200B;

     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]： `Ad Clicks`

   * [!UICONTROL Metric]： `Ad Impressions`

   * [!UICONTROL Formula]： `(H / I)`
   * &#x200B;

     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]： `(A / H)`
   * &#x200B;

     [!UICONTROL Format]: `Currency`

* 量度`A`： `Ad Spend` （隐藏）
* 量度`B`： `Ad customer acquisitions`
* 量度`C`： `Average LTV`
* 量度`D`： `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL 公式]: `CAC`
* [!UICONTROL Formula]： `Avg return`
* [!UICONTROL Formula]： `Ads ROI`
* 量度`H`： `adClicks`
* 量度`I`： `Impressions`
* &#x200B;
  [!UICONTROL 公式]: `CTR`
* &#x200B;
  [!UICONTROL 公式]: `CPC`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 间隔]: `None`
* &#x200B;
  [!UICONTROL 分组依据]: `campaign` (将“客户的第一个订单”促销活动用于非广告支出表量度)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

如果您在构建此分析时遇到任何问题，或只是想与专业服务团队接洽，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)。

### 相关

* [在 [!DNL Google Analytics]中进行UTM标记的最佳实践](../../best-practices/utm-tagging-google.md)
* [ [!DNL Google Analytics] UTM归因如何工作？](../analysis/utm-attributes.md)
