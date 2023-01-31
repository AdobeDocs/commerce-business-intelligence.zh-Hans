---
title: 商务流失率
description: 了解如何生成和分析您的商务流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 流失率

在本主题中，我们演示了如何计算 **流失率** , **商务客户**. 与SaaS或传统订阅公司不同，商务客户通常没有具体的 **&quot;流失事件&quot;** 以表明他们不应再计入您的活跃客户。 因此，下面的说明允许您根据客户上次订购后经过的确定时间，将客户定义为“已更改”。

![](../../assets/Churn_rate_image.png)

许多客户希望在开始概念化 **时间范围** 他们应根据其数据使用。 如果要使用历史客户行为来定义此项 **流失时间**，您可能需要熟悉 [定义流失](../analysis/define-cust-churn.md) 文章。 然后，您可以按照以下说明将公式中的结果用于流失率。

## 计算列

要创建的列

* **`customer_entity`** 表
* **`Customer's last order date`**
   * 选择 [!UICONTROL definition]: `Max`
   * 选择 [!UICONTROL table]: `sales_flat_order`
   * 选择 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 选择 [!UICONTROL definition]: `Age`
   * 选择 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 量度

* **新客户（按首次订购日期）**
   * 我们计数的客户

>[!NOTE]
>
>此量度可能已存在于您的帐户中。

* 在 **`customer_entity`** 表
* 此量度执行 **计数**
* 在 **`entity_id`** 列
* 由 **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新客户（按上次订单日期）**
   * 我们计数的客户

>[!NOTE]
>
>此量度可能已存在于您的帐户中。

* 在 **`customer_entity`** 表
* 此量度执行 **计数**
* 在 **`entity_id`** 列
* 由 **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **流失率**
   * [!UICONTROL Metric]:新客户（按首次订购日期）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 自客户上次订购日期后经过的秒数>= [您为被教育的客户自定义的截止日期&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *量度 `A`:`New customers cumulative`*
* *量度 `B`:`Churned customers by last order date`*
* *量度 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

以下是一些常见的月份>第二次转化，但是Google提供了其他值，包括您可能要查找的任何自定义值的周>秒转化。

| **月** | **秒** |
|---|---|
| 3 | 777.6万 |
| 6 | 一千五百五十五万两千 |
| 9 | 两千三百三十二万八千 |
| 12 | 3110.4万 |

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与上述示例仪表板类似。
