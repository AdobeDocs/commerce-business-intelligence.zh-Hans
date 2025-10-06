---
title: Commerce流失
description: 了解如何生成和分析Commerce客户流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 客户流失率

本主题演示如何计算&#x200B;**商务客户**&#x200B;的&#x200B;**客户流失率**。 与SaaS或传统订阅公司不同，商业客户通常没有具体的&#x200B;**“流失事件”**&#x200B;来向您显示他们不再计入您的活跃客户。 因此，您可以通过下面的说明，根据自上次订购以来经过的时间，将客户定义为“已流失”。

![显示一段时间内客户维系情况的客户流失率可视化图表](../../assets/Churn_rate_image.png)

许多客户都希望获得帮助，以便开始根据自己的数据来构想他们应该使用的&#x200B;**时间范围**。 如果要使用历史客户行为来定义此&#x200B;**客户流失时间范围**，您可能需要熟悉[定义流失](../analysis/define-cust-churn.md)主题。 然后，您可以在下面的说明中使用客户流失率公式中的结果。

## 计算列

要创建的列

* **`customer_entity`**&#x200B;表
* **`Customer's last order date`**
   * 选择[!UICONTROL definition]： `Max`
   * 选择[!UICONTROL table]： `sales_flat_order`
   * 选择[!UICONTROL column]： `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]： `Orders we count`

* **`Seconds since customer's last order date`**
   * 选择[!UICONTROL definition]： `Age`
   * 选择[!UICONTROL column]： `Customer's last order date`

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 量度

* **新客户（按第一订单日期）**
   * 被计数的客户

>[!NOTE]
>
>此量度可能存在于您的帐户中。

* 在&#x200B;**`customer_entity`**&#x200B;表中
* 此量度执行&#x200B;**计数**
* 在&#x200B;**`entity_id`**&#x200B;列上
* 按&#x200B;**`Customer's first order date`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

* **新客户（按上次订购日期）**
   * 被计数的客户

  >[!NOTE]
  >
  >此量度可能存在于您的帐户中。

* 在&#x200B;**`customer_entity`**&#x200B;表中
* 此量度执行&#x200B;**计数**
* 在&#x200B;**`entity_id`**&#x200B;列上
* 按&#x200B;**`Customer's last order date`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 报告

* **客户流失率**
   * [!UICONTROL Metric]：新客户（按第一订单日期）
   * [!UICONTROL Filter]： `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]： `New customers (by last order date)`
   * [!UICONTROL Filter]：
   * 自客户上次订购日期以来的秒数>= [您为流失客户自定义的截止日期&#x200B;]&#x200B;**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]： `New customers (by last order date)`
   * [!UICONTROL Filter]： `Lifetime number of orders Greater Than 0`
   * &#x200B;
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]： `(B / ((A + B) - C)`
   * &#x200B;
     [!UICONTROL Format]: Percentage

* *量度`A`：`New customers cumulative`*
* *量度`B`：`Churned customers by last order date`*
* *量度`C`：`Customers by last order date cumulative`*
* *`Formula`：`Repeat order probability`*
* *`Time period`：`All time (or custom range)`*
* *`Group by`：`Customer's order number`*
* *`Chart Type`：`Column`*

以下是一些常见的月>秒转化，但google提供了其他值，包括您可能要查找的任何自定义值的周>秒转化。

| **个月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于上面的示例仪表板。
