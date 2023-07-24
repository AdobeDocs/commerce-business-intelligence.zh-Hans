---
title: 分析退货单
description: 了解如何设置一个仪表板，用于提供对商店回报的详细分析。
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 退货单

本主题将演示如何设置一个功能板，用于提供对商店退货的详细分析。

![](../../assets/detailed-returns-dboard.png)

在开始之前，您必须是 [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 客户，并且应该确保贵公司使用的是 `enterprise\_rma` 返回表。

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

要跟踪的列

* **`enterprise_rma`** 或 **`rma`** 表
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** 或 **`rma_item_entity`** 表
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

要创建的筛选器集

* **`enterprise_rma`** 表
* 筛选器集名称： `Returns we count`
* 筛选器集逻辑：
   * 占位符 — 在此处输入自定义逻辑

* **`enterprise_rma_item_entity`** 表
* 筛选器集名称： `Returns items we count`
* 筛选器集逻辑：
   * 占位符 — 在此处输入自定义逻辑

### 计算列

要创建的列

* **`enterprise_rma`** 表
* **`Order's created at`**
* 选择定义： `Joined Column`
* [!UICONTROL Create Path]:
* 
  [!UICONTROL Many]: `enterprise_rma.order_id`
* 
  [!UICONTROL One]: `sales_flat_order.entity_id`

* 选择 [!UICONTROL table]： `sales_flat_order`
* 选择 [!UICONTROL column]： `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 选择定义： `Joined Column`
* 选择 [!UICONTROL table]： `sales_flat_order`
* 选择 [!UICONTROL column]： `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** 由分析师创建，作为您的一部分 `[RETURNS ANALYSIS]` 票证

* **`enterprise_rma_item_entity`** 表
* **`return_date_requested`**
* 选择定义： `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* 选择 [!UICONTROL table]： `enterprise_rma`
* 选择 [!UICONTROL column]： `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** 由分析师创建，作为您的一部分 `[RETURNS ANALYSIS]` 票证

* **`sales_flat_order`** 表
* **`Order contains a return? (1=yes/0=No)`**
* 选择定义： `Exists`
* 选择 [!UICONTROL table]： `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** 由分析师创建，作为您的一部分 `[RETURNS ANALYSIS]` 票证
* **`Customer's previous order contains return? (1=yes/0=no)`** 由分析师创建，作为您的一部分 `[RETURNS ANALYSIS]` 票证

>[!NOTE]
>
>如果您只想分析秒数到分辨率或秒数到首次响应的营业时间，请在请求票证时告知分析人员。

### 量度

* **返回**
* 在 **`enterprise_rma`** 表
* 此量度执行 **计数**
* 在 **`entity_id`** 列
* 排序依据 **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返回的项目**
* 在 **`enterprise_rma_item_entity`** 表
* 此量度执行 **总和**
* 在 **`qty_approved`** 列
* 排序依据 **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返回的项目总值**
* 在 **`enterprise_rma_item_entity`** 表
* 此量度执行 **总和**
* 在 **`Returned item total value (qty_returned * price)`** 列
* 排序依据 **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **订单与退货之间的平均间隔时间**
* 在 **`enterprise_rma`** 表
* 此量度执行 **Average**
* 在 **`Time between order's created_at and date_requested`** 列
* 排序依据 **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>确保 [将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。

### 报告

* **返回后重复排序的概率**
* 量度 `A`： `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* 量度 `B`： `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：重复订单概率
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [！UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
  [！UICONTROL图表类型]: `Bar`

* **平均返回时间（所有时间）**
* 量度 `A`： `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
  [！UICONTROL间隔]: `None`
* 
  [！UICONTROL图表类型]: `Number`

* **具有退货的订单百分比**
* 量度 `A`： `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* 量度 `B`： `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：具有退货的订单百分比
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [！UICONTROL间隔]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **按月返回收入**
* 量度 `A`： `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 
  [！UICONTROL图表类型]: `Line`

* **已退货且不再购买的客户**
* 量度 `A`： `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
  [！UICONTROL间隔]: `None`
* 
  [！UICONTROL分组依据]: `Customer_email`
* 
  [！UICONTROL图表类型]: `Table`

* **按物料列出的退货率**
* 量度 `A`： `Returned items` （隐藏）
* [!UICONTROL Metric]：返回的项目

* 量度 `B`： `Items sold` （隐藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [！UICONTROL间隔]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
  [！UICONTROL图表类型]: `Table`

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于上述示例仪表板。

如果您在构建此分析时遇到任何问题，或者希望与专业服务团队接洽， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
