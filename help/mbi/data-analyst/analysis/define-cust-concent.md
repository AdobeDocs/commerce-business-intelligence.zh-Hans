---
title: 定义客户集中度
description: 了解如何设置功能板，以帮助您衡量总收入在客户群中的分配方式。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 客户集中度

在本文中，我们演示了如何设置功能板，以帮助您衡量如何在客户群中分配总收入。 了解什么百分比的客户贡献了多少收入百分比，并创建分段列表以向最佳市场贡献和留住高贡献的客户。

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

您首先需要上载一个仅包含值为1的主键的文件。 这将允许为分析创建一些必要的计算列。

您可以利用 [文件上载程序](../importing-data/connecting-data/using-file-uploader.md) 以及下图来设置文件格式。

## 计算列

如果您位于原始架构上(例如，如果您没有 `Data Warehouse Views` 选项 `Manage Data` 菜单)，则需要联系我们的支持团队以构建以下列。 在新架构上，可以通过 `Manage Data > Data Warehouse` 页面。 详细说明如下。

如果您的企业允许客人订购，则会有进一步的区别。 如果存在，则可以忽略 `customer_entity` 表。 如果不允许来宾订单，请忽略 `sales_flat_order` 表。

要创建的列

* `Sales_flat_order/customer_entity` 表
* （输入） `reference`
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `entity_id`
* [!UICONTROL Calculation]:- **如果A为null，则结束1**
* [!UICONTROL Datatype]:- `Integer`

* `Customer concentration` 表(这是您刚刚上传的文件，其中包含 `1`)
* 客户数量
* [!UICONTROL Column type]:- `Many to One > Count Distinct`
* 路径 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 选定列 —  `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* `customer_entity` 表
* 客户数量
* [!UICONTROL Column type]:- `One to Many > JOINED_COLUMN`
* 路径 —  `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 选定列 —  `Number of customers`

* （输入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]:- `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`

* 客户的收入百分比
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **当A为空时，则为空(A/B)* 100结束&#x200B;**
* [!UICONTROL Datatype]:- `Decimal`

* `Sales_flat_order` 表
* 客户数量
* [!UICONTROL Column type]:- `One to Many > JOINED_COLUMN`
* 路径 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 选定列 —  `Number of customers`

* （输入）按客户生命周期收入排名
* [!UICONTROL Column type]:- `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`
* 过滤器 —  `Customer's order number = 1`

* 客户的收入百分比
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **当A为空时，则为空(A/B)* 100结束&#x200B;**
* [!UICONTROL Datatype]:- `Decimal`

>[!NOTE]
>
>使用的百分位数甚至是客户的拆分，表示客户群的第X个百分位数。 每个客户都将与一个介于1到100之间的整数关联，该整数可以视为其生命周期收入 *排名*. 例如，如果特定客户的收入百分位数为 **5**，则此客户位于 ***第5个百分位数*** 所有客户的收入。

## 量度

* **客户生命周期总值**
* 在 `customer_entity` 表
* 此量度执行 **总和**
* 在 `Customer's lifetime revenue` 列
* 由 `Customer's first order date` timestamp

## 报表

* **客户集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL组依据]: `Independent`
* 量度 `A`: `Total customer lifetime revenue by percentile`
* 量度 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 显示顶部/底部： `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **前10%浓度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 量度 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [!UICONTROL组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **只需一次购买，即可达到最低50%的集中度**

* 量度 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [!UICONTROL组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最低10%浓度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 量度 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [!UICONTROL组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与上述示例仪表板类似。

如果您在构建此分析时遇到任何问题，或者只想与我们的专业服务团队接洽， [联系支持](../../guide-overview.md).
