---
title: 定义客户流失
description: 了解如何设置仪表板来帮助您定义事务型客户的流失。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/eDJBh7FlhuKjBa5ft4sqAfZavmBk4V9m-Iu-26cG2VI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 482
ht-degree: 0%

---

# 事务性客户流失

本主题演示如何设置功能板，帮助您定义事务型客户的流失。

![显示流失率和保留量度的客户流失仪表板](../../assets/churn-deashboard.png)

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
* 
  [！UICONTROL公式]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]： `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **重复订单的概率自订单**&#x200B;以来已给定的月份
* 量度A：按上个订单后间隔的月份重复订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]： `Customer's order number greater than 1`

* 量度B：按订购后月份列出的最后订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]： `Is customer's last order? (Yes/No) = Yes`

* 量度C：所有时间重复订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]： `Customer's order number greater than 1`

* 
  [！UICONTROL分组依据]: `Independent`

* 量度D：所有时间最后订单（隐藏）
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]： `Is customer's last order? (Yes/No) = Yes`

* 
  [！UICONTROL分组依据]: `Independent`

* [!UICONTROL Formula]：初始重复顺序概率
* 
  [！UICONTROL公式]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]： `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Months since previous order`
* 显示top.bottom：前24个类别，按类别名称排序

* 
  [!UICONTROL Chart type]: `Line`

初始重复订单概率报表表示“重复订单总数/订单总数”。 每个顺序都是产生重复顺序的机会；重复顺序的数量是那些实际发生的顺序的子集。

您使用的公式简化为（X个月后发生的重复订单总数）/（至少是X个月前的订单总数）。 它向我们表明，从历史上看，由于自下订单以来已经过了X个月，用户再次下订单的可能性为Y%。

构建功能板后，最常见的问题是：如何使用它来确定流失阈值？

**对此没有“一个正确答案”。**&#x200B;但是，Adobe建议查找直线与初始重复概率的一半值相交的点。 在这个时候，您可以说“如果用户要重复订单，他们现在可能已经完成了。” 最终，目标是选择适合从“保留”工作切换到“重新激活”工作的阈值。

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能与页面顶部的图像类似

如果您在构建此分析时遇到任何问题，或只是想与专业服务团队接洽，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
