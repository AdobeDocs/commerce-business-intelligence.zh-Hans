---
title: 定义客户集中度
description: 了解如何设置一个仪表板，帮助您衡量总收入如何在客户群中分配。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# 客户集中

本主题演示如何设置一个仪表板，帮助您衡量总收入如何在客户群中分配。 了解客户贡献了多少百分比的收入，并创建分段列表以最好地向市场推广并留住贡献最多的客户。

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

您需要首先上传一个文件，该文件只包含值为1的主键。 这允许为分析创建一些必要的计算列。

您可以使用 [文件上传程序](../importing-data/connecting-data/using-file-uploader.md) 和下图来格式化您的文件。

## 计算列

如果您使用的是原始架构(例如，如果您没有 `Data Warehouse Views` 下的选项 `Manage Data` 菜单)，您希望联系支持团队以构建以下列。 在新架构上，这些列可以从 `Manage Data > Data Warehouse` 页面。 详细说明如下。

如果贵公司允许客人下单，则需作进一步区分。 如果是这样，您可以忽略的所有步骤 `customer_entity` 表格。 如果不允许来宾订单，请忽略 `sales_flat_order` 表格。

要创建的列

* `Sales_flat_order/customer_entity` 表
* （输入） `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]： - **A为null时为null的情况，否则1结束**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` 表(这是您上传的文件，编号为 `1`)
* 客户数量
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* 路径 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 选定的列 —  `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* `customer_entity` 表
* 客户数量
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路径 —  `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 选定的列 —  `Number of customers`

* （输入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`

* 客户的收入百分位数
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]： - **当A为null然后为null时的情况，否则(A/B)* 100结束&#x200B;**
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` 表
* 客户数量
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路径 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 选定的列 —  `Number of customers`

* （输入）按客户存留期收入排名
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`
* 筛选条件 —  `Customer's order number = 1`

* 客户的收入百分位数
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]： - **当A为null然后为null时的情况，否则(A/B)* 100结束&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用的百分位数是甚至客户分段，代表客户群的第X个百分位数。 每个客户都关联一个1到100的整数，可将其视为其生命周期收入 *排名*. 例如，如果特定客户的客户收入百分位数为 **5**，该客户位于 ***第5个百分位数*** 终生收入而言，所有客户之总收入约为25,000港元。

## 量度

* **客户存留期值总计**
* 在 `customer_entity` 表
* 此量度执行 **总和**
* 在 `Customer's lifetime revenue` 列
* 排序依据 `Customer's first order date` 时间戳

## 报告

* **客户集中**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [！UICONTROL分组依据]: `Independent`
* 量度 `A`： `Total customer lifetime revenue by percentile`
* 量度 `B`： `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 显示顶部/底部： `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **前10%浓度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 量度 `A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [！UICONTROL分组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **仅需一次购买即可达到最低50%的集中度**

* 量度 `A`： `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [！UICONTROL分组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **底部10%浓度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 量度 `A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* 
   [！UICONTROL分组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于上述示例仪表板。

如果您在构建此分析时遇到任何问题，或者只是想让专业服务团队参与进来， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
