---
title: 优惠券性能
description: 了解如何分析优惠券性能。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---

# 高级优惠券代码分析

了解业务的优惠券性能是划分订单细分并更好地了解客户的有趣方式。 本文将指导您完成创建分析的步骤，以了解您通过使用优惠券获得哪些客户，他们如何执行和跟踪一般优惠券使用情况。

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

第一步，您需要确保将以下列同步到您的Data warehouse。 如果没有，请继续并跟踪，方法是导航到“管理数据”>“Data warehouse”，然后同步以下内容：

* **sales\_flat\_order** 表
* **优惠券\_code**
* **base\_discount\_amount**

## 计算列

要创建列，而不考虑来宾订单策略：

* `sales\_flat\_order` 表
* **订购是否应用了优惠券？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:在 `A` 表示为空 `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id — 优惠券代码**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]:字符串
   * [!UICONTROL Calculation]:: `concat(A,' - ',B)`


* **具有此优惠券的订单数**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * 事件所有者：`INPUT customer_id - coupon code`
   * 事件排名： `created\_at`
   * [!UICONTROL Filters]: `Orders we count` 筛选器集

不支持来宾订单时要创建的其他列：

* `customer\_entity` 表
   * **客户的首笔订购中包括优惠券？ （优惠券/无优惠券）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * 选择 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **客户首次订购的优惠券**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 选择 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **客户使用的优惠券的存留期数**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **优惠券客户或非优惠券客户获取客户**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **A=“优惠券”，然后“优惠券客户”，其他“非优惠券客户”结束时的用例**
   * **具有优惠券的客户订单百分比**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]:: `Decimal`
      * [!UICONTROL Calculation]: **A为null或B为null或B=0时，A/B结束**
   * **客户的优惠券使用情况**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]: **当A=0时A为null，当A&lt;0.5时为“从不使用优惠券”，当A=0.5时为“大部分全价”，当A=1时为“仅优惠券”，当A>0.5时为“大部分优惠券”，当A=0.5时为“大部分未使用优惠券”时为“大部分全价”**









* `sales\_flat\_order` 表
   * **客户的首次订购中是否包含优惠券？ （优惠券/无优惠券）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 选择 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **客户首次订购的优惠券**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * 选择 [!UICONTROL column]: `Customer's first order coupon?`


不支持来宾订单时要创建的其他列：

* `sales\_flat\_order` 表
   * **客户的首笔订购中包括优惠券？ （优惠券/无优惠券）** **-** 由分析师创建，作为\[优惠券分析\]票证的一部分
   * **客户首次订购的优惠券**{:}**-** 由分析师创建，作为\[优惠券分析\]票证的一部分

* **客户使用的优惠券的存留期数**{:}**-** 由分析师创建，作为\[优惠券分析\]票证的一部分
* **优惠券客户或非优惠券客户获取客户**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **A=“优惠券”，然后“优惠券客户”，其他“非优惠券客户”结束时的用例**


* **具有优惠券的客户订单百分比**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]:: `Decimal`
   * [!UICONTROL Calculation]: **A为null或B为null或B=0时，A/B结束**


* **客户的优惠券使用情况**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]: **当A=0时A为null，当A&lt;0.5时为“从不使用优惠券”，当A=0.5时为“大部分全价”，当A=1时为“仅优惠券”，当A>0.5时为“大部分优惠券”，当A=0.5时为“大部分未使用优惠券”时为“大部分全价”**


## 量度

* **优惠券折扣金额**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表
* 此量度执行 **总和**
* 在 `discount\_amount` 列
* 由 `created\_at` timestamp
* [!UICONTROL Filter]:

* **使用的优惠券数量**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* 在 `sales\_flat\_order` 表
* 此量度执行 **计数**
* 在 `entity\_id` 列
* 由 `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **已购入和非已购入优惠券的客户的百分比**
   * [!UICONTROL Metric]: `New customers`

* 量度 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* 

   [!UICONTROL图表类型]: `Pie`

* **购入优惠券和未购买优惠券的客户数量**
   * [!UICONTROL Metric]: `New customers`

* 量度A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` 或 `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均存留期收入：优惠券Acq。 （90天以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=优惠券

* 量度 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Scalar`

* **平均存留期收入：无优惠券Acq。 （90天以上）**
   * [!UICONTROL Metric]:平均存留期收入
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=无优惠券

* 量度 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Scalar`

* **按订单优惠券划分的平均存留期收入**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 量度 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL图表类型]: `Column`

>[!NOTE]
>
>如果您有大量优惠券代码（与我们的许多客户一样），您将需要应用“前/后”(Top/Bottom)，如按平均生命周期收入排序的“前10”

* **重复顺序可能性：优惠券购买**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=优惠券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=优惠券
      * 客户的最后订单吗？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 从 `Customer's by lifetime orders` 图表。 在查看图表时，作为一项良好的规则，我们通常会查找存储段中有30个或更多客户的订单号。 根据您的数据集，此数字可能会很大，因此您可以随时添加1-10。


* 量度 `A`: `Number of orders`
* 量度 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **重复顺序概率：非优惠券收购**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=无优惠券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户的首笔订单包括优惠券（优惠券/无优惠券）=无优惠券
      * 客户的最后订单吗？ =否
   * 
      [!UICONTROL公式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 从 `Customer's by lifetime orders` 图表或1-5。



* 量度 `A`: `Number of orders`
* 量度 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **优惠券购买客户的优惠券使用率（重复订单）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 优惠券客户或非优惠券客户获取客户=优惠券客户获取
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户订单号> 1
      * 客户的首笔订购中包括优惠券？ （优惠券/无优惠券）=优惠券
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 客户订单号> 1
      * 客户的首笔订购中包括优惠券？ （优惠券/无优惠券）=优惠券
      * 订购是否应用了优惠券？ （优惠券/无优惠券）=优惠券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 量度 `A`: `Coupon-acquired customers`
* 量度 `B`: `Number of repeat orders`
* 量度 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Table` (可以转换此表格，以便更好地显示)

* **非优惠券购买客户的优惠券使用率（重复订单）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 优惠券客户或非优惠券客户获取客户=非优惠券客户获取
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户订单号> 1
      * 客户的首笔订购中包括优惠券？ （优惠券/无优惠券）=无优惠券
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户订单号> 1
      * 客户的首笔订购中包括优惠券？ （优惠券/无优惠券）=无优惠券
      * 订购是否应用了优惠券？ （优惠券/无优惠券）=优惠券
   * 
      [!UICONTROL公式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* 量度 `A`: `Non-coupon-acquired customers`
* 量度 `B`: `Number of repeat orders`
* 量度 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Table` (可以转换此表格，以便更好地显示)

* **优惠券使用详细信息（首次订购）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 客户订单编号= 1
      * 此优惠券的订单数超过10
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 客户订单编号= 1
      * 此优惠券的订单数超过10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 客户订单编号= 1
      * 此优惠券的订单数超过10
   * [!UICONTROL Formula]: `B-C` （如果C为负）；B+C（如果C为正）
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 客户订单编号= 1
      * 此优惠券的订单数超过10




* 量度 `A`: `First time orders (FTO)`
* 量度 `B`: `Revenue from FTO`
* 量度 `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 量度 `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL图表类型]: `Table`
>[!NOTE]
>
>“具有此优惠券的订单数”的数量为10是任意的。 请随时为此过滤器使用最合适的数量。

* **具有优惠券的订单数（所有时间）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 量度 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Scalar`

* **具有优惠券的订单的净收入（始终）**
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 订购是否应用了优惠券？ （优惠券/无优惠券）=优惠券

* 量度 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Scalar`

* **优惠券折扣（全时）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 量度 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* 

   [!UICONTROL图表类型]: `Scalar`

* **具有和没有优惠券的订单数**
   * [!UICONTROL Metric]: `Number of orders`

* 量度 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **重复用户的优惠券使用情况**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 客户的生命周期订单数> 1

* 量度 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL图表类型]: `Pie`

* **优惠券使用情况详细信息**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * 此优惠券的订单数超过10
   * 
      [!UICONTROL量度]: `Revenue`
   * [!UICONTROL Filter]:
      * 此优惠券的订单数超过10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 此优惠券的订单数超过10
   * [!UICONTROL Formula]: `B-C` (如果 `C` 为负数); `B+C` (如果 `C` 为正值)
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (如果 `C` 为负数); `C/(B+C)` (如果 `C` 为正值)
   * 

      [!UICONTROL格式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 此优惠券的订单数超过10
   * 
      [!UICONTROL公式]: `C/A`
   * 

      [!UICONTROL格式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * 此优惠券的订单数超过10





* 量度 `A`: `Number of orders`
* 量度 `B`: `Net revenue from orders`
* 量度 `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 量度 `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 量度 `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL图表类型]: `Table`

>[!NOTE]
>
>“具有此优惠券的订单数”的数量为10是任意的。 请随时为此过滤器使用最合适的数量。

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与页面顶部的图像类似。

如果您在构建此分析时遇到任何问题，或者只想与我们的专业服务团队接洽， [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
