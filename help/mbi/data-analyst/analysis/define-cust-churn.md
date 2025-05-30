---
title: 定义客户流失
description: 了解如何设置仪表板来帮助您定义事务型客户的流失。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 事务性客户流失

本主题演示如何设置功能板，帮助您定义事务型客户的流失。

![](../../assets/churn-deashboard.png)

此分析包含[高级计算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 计算列

要创建的列

* `customer_entity`表
* `Customer's lifetime number of orders`
* 选择定义： `Count`
* 选择[!UICONTROL table]： `sales_flat_order`
* 选择[!UICONTROL column]： **`entity_id`**
* [!UICONTROL Path]： sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]：
* 已计数的订单

* `sales_flat_order`表
* `Customer's lifetime number of orders`
* 选择定义：联接列
* 选择[!UICONTROL table]： `customer_entity`
* 选择[!UICONTROL column]： `Customer's lifetime number of orders`
* [!UICONTROL Path]： `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]： `Orders we count`

* `Seconds since created_at`
* 选择定义： `Age`
* 选择[!UICONTROL column]： `created_at`

* **`Customer's order number`**&#x200B;由分析师创建，作为&#x200B;**[DEFINING CHURN]**&#x200B;票证的一部分
* **`Is customer's last order`**&#x200B;由分析师创建，作为&#x200B;**[DEFINING CHURN]**&#x200B;票证的一部分
* **`Seconds since previous order`**&#x200B;由分析师创建，作为&#x200B;**[DEFINING CHURN]**&#x200B;票证的一部分
* **`Months since order`**&#x200B;由分析师创建，作为&#x200B;**[DEFINING CHURN]**&#x200B;票证的一部分
* **`Months since previous order`**&#x200B;由分析师创建，作为&#x200B;**[DEFINING CHURN]**&#x200B;票证的一部分

## 量度

无新量度！

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 报告

* **初始重复顺序概率**
* 指标A：所有时间重复订单
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]： `Customer's order number greater than 1`

* 量度B：所有时间订单
* [!UICONTROL Metric]：订单数

* [!UICONTROL Formula]：初始重复顺序概率
* &#x200B;
  [!UICONTROL 公式]: `A/B`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart type]: `Scalar`

* **重复订单的概率自订单**&#x200B;以来已给定的月份
* 量度A：按上个订单后间隔的月份重复订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]： `Customer's order number greater than 1`

* 量度B：按订购后月份列出的最后订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]： `Is customer's last order? (Yes/No) = Yes`

* 量度C：所有时间重复订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]： `Customer's order number greater than 1`

* &#x200B;
  [!UICONTROL 分组依据]: `Independent`

* 量度D：所有时间最后订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]： `Is customer's last order? (Yes/No) = Yes`

* &#x200B;
  [!UICONTROL 分组依据]: `Independent`

* [!UICONTROL Formula]：初始重复顺序概率
* &#x200B;
  [!UICONTROL 公式]: `(C-A)/(C+D-A-B)`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Months since previous order`
* 显示top.bottom：前24个类别，按类别名称排序

* &#x200B;
  [!UICONTROL Chart type]: `Line`

初始重复订单概率报表表示“重复订单总数/订单总数”。 每个顺序都是产生重复顺序的机会；重复顺序的数量是那些实际发生的顺序的子集。

您使用的公式简化为（X个月后发生的重复订单总数）/（至少是X个月前的订单总数）。 它向我们表明，从历史上看，由于自下订单以来已经过了X个月，用户再次下订单的可能性为Y%。

构建功能板后，最常见的问题是：如何使用它来确定流失阈值？

**对此没有“一个正确答案”。**&#x200B;但是，Adobe建议查找线条与初始重复概率比率一半的值相交的点。 在这个时候，您可以说“如果用户要重复订单，他们现在可能已经完成了。” 最终，目标是选择适合从“保留”工作切换到“重新激活”工作的阈值。

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能与页面顶部的图像类似

如果您在构建此分析时遇到任何问题，或只是想与专业服务团队接洽，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)。
