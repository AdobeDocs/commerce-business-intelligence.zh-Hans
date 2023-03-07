---
title: 营销ROI
description: 了解如何设置一个仪表板来跟踪您的渠道分析，包括汇总的ROI和按营销活动。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# 营销ROI

>[!NOTE]
>
>本文包含有关使用原始架构和新架构的客户端的说明。 您位于 [新架构](../../administrator/account-management/new-architecture.md) 如果您在主工具栏中选择“管理数据”后有“Data warehouse视图”部分可用。

如果您正在在线广告上花钱，则希望跟踪您在这方面的投资回报，并在进一步投资方面做出数据驱动型决策。 本文演示了如何设置一个仪表板来跟踪您的渠道分析，包括汇总的ROI和按营销活动。

![](../../assets/Marketing_dashboard_example.png)

在开始之前，您想要连接 [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md)， [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)、和 [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) 帐户，并引入任何其他在线广告支出数据。 此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 统一表

**原始架构：** 将来自各种来源(例如 [!DNL Facebook Ads] 或 [!DNL Google Adwords])，Adobe建议创建 **统一表** 你广告花费的总和。 您需要一位分析师为您完成此步骤。 如果你没有， [提出支持请求](../../guide-overview.md) 带有主题 `[MARKETING ROI ANALYSIS]`，Analyst将创建此表。

**新架构：** 您可以按照以下示例进行操作： [此分析库](../../data-analyst/data-warehouse-mgr/create-dw-views.md) 主题。 在新体系结构中，统一表现在称为Data warehouse视图。

## 计算列

要创建的列

* **`Consolidated Digital Ad Spend`** 表
* **`Campaign name`** 由分析师创建，作为您的一部分 **[营销ROI分析]** 票证

>[!NOTE]
>
>请参阅上文，了解新架构的差异。

**原有和新的体系结构：**

* **`sales_flat_order`** 表
   * **`Order's GA campaign`**
      * 选择定义： `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * 选择 [!UICONTROL table]： `ecommerce####`
      * 选择 [!UICONTROL column]： `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * 选择定义：联接列
      * 选择 [!UICONTROL table]： `ecommerce####`
      * 选择 [!UICONTROL column]： `medium`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce####.transactionId
   * **`Order's GA source`**
      * 选择定义：联接列
      * 选择 [!UICONTROL table]： `ecommerce####`
      * 选择 [!UICONTROL column]： `source`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce####.transactionId ^




* **`customer_entity`** 表
* **`Customer's first order GA campaign`**
   * 选择定义： `Max`
   * 选择 [!UICONTROL table]： `sales_flat_order`
   * 选择 [!UICONTROL column]： `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 选择定义： `Max`
   * 选择 [!UICONTROL table]： `sales_flat_order`
   * 选择 [!UICONTROL column]： `Order's GA source`
   * [!UICONTROL Path]： sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 选择定义： `Max`
   * 选择 [!UICONTROL table]： `sales_flat_order`
   * 选择 [!UICONTROL column]： `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** 表
* **`Customer's first order GA campaign`**
   * 选择定义： `Joined Column`
   * 选择 [!UICONTROL table]： `customer_entity`
   * 选择 [!UICONTROL column]： `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 选择定义：联接列
   * 选择 [!UICONTROL table]： `customer_entity`
   * 选择 [!UICONTROL column]： `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 选择定义： `Joined Column`
   * 选择 [!UICONTROL table]： `customer_entity`
   * 选择 [!UICONTROL column]： `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 量度

* **广告支出**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此量度执行 **总和**
* 在 **`adCost`** 列
* 排序依据 **`date`** 时间戳

* **广告展示次数**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此量度执行 **总和**
* 在 **`Impressions`** 列
* 排序依据 **`Month`** 时间戳

* **广告点击次数**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此量度执行 **总和**
* 在 **`adClicks`** 列
* 排序依据 **`Month`** 时间戳

>[!NOTE]
>
>确保 [将所有新列作为维度添加到量度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。

## 报告

* **广告花费（所有时间）**
   * [!UICONTROL Metric]：广告支出

* 量度 `A`：广告支出
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL间隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **广告客户获取（所有时间）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]

* 量度 `A`： `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL间隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **广告ROI**
   * [!UICONTROL Metric]：广告支出

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均生命周期收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* 量度 `A`： `Ad Spend (hide)`
* 量度 `B`： `Ad customer acquisitions (hide)`
* 量度 `C`： `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL间隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **按Ga中等深浅**
   * 

      [！UICONTROL量度]: `Orders`

* 量度 `A`： `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **按营销活动显示的广告ROI**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均生命周期收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均生命周期订单数
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 筛选器逻辑： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* 量度 `A`： `Ad Spend` （隐藏）
* 量度 `B`： `Ad customer acquisitions`
* 量度 `C`： `Average LTV`
* 量度 `D`： `Average lifetime # of orders`
* 
   [！UICONTROL公式]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* 量度 `H`： `adClicks`
* 量度 `I`： `Impressions`
* 
   [！UICONTROL公式]: `CTR`
* 
   [！UICONTROL公式]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL间隔]: `None`
* 
   [！UICONTROL分组依据]: `campaign` (将“客户的第一个订单”促销活动用于非广告支出表格量度)
* 

   [!UICONTROL Chart Type]: `Table`

如果您在构建此分析时遇到任何问题，或者只是想让专业服务团队参与进来， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### 相关

* [中的UTM标记最佳实践 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [如何 [!DNL Google Analytics] UTM归因工作？](../analysis/utm-attributes.md)
