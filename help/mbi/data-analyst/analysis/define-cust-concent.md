---
title: 定义客户集中度
description: 了解如何设置一个仪表板，帮助您衡量总收入在客户群中的分配情况。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 客户集中

本主题将演示如何设置一个仪表板，帮助您衡量总收入如何在客户群之间分配。 了解客户贡献了多少百分比的收入，并创建分段列表以最好地向市场推广并留住做出贡献最多的客户。

此分析包含[高级计算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 快速入门

您需要首先上传一个文件，其中只包含值为1的主键。 这允许为分析创建一些必要的计算列。

您可以使用[文件上载程序](../importing-data/connecting-data/using-file-uploader.md)以及下面的图像来格式化文件。

## 计算列

如果您使用的是原始架构（例如，如果您的`Data Warehouse Views`菜单下没有`Manage Data`选项），则您需要联系支持团队以构建以下列。 在新架构上，可从`Manage Data > Data Warehouse`页面创建这些列。 下面提供了详细说明。

如果您的企业允许客户订购，则需作进一步的区分。 如果是，则可以忽略`customer_entity`表的所有步骤。 如果不允许来宾订单，请忽略`sales_flat_order`表的所有步骤。

要创建的列

* `Sales_flat_order/customer_entity`表
* （输入） `reference`
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `entity_id`
* [!UICONTROL Calculation]： - **当A为null时为null，否则为1结束**
* [!UICONTROL Datatype]： - `Integer`

* `Customer concentration`表（这是您上传的编号为`1`的文件）
* 客户数量
* [!UICONTROL Column type]： - `Many to One > Count Distinct`
* 路径 — `sales_flat_order.(input) reference > Customer Concentration.Primary Key`或`customer_entity.(input)reference > Customer Concentration.Primary Key`
* 选定的列 — `sales_flat_order.customer_email`或`customer_entity.entity_id`

* `customer_entity`表
* 客户数量
* [!UICONTROL Column type]： - `One to Many > JOINED_COLUMN`
* 路径 — `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 选定的列 — `Number of customers`

* （输入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]： - `Same table > Event Number`
* 事件所有者 — `Number of customers`
* 事件排名 — `Customer's lifetime revenue`

* 客户的收入百分位数
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `(input) Ranking by customer lifetime revenue`，`Number of customers`
* [!UICONTROL Calculation]： - **当A为null时为null，否则为null (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]： - `Decimal`

* `Sales_flat_order`表
* 客户数量
* [!UICONTROL Column type]： - `One to Many > JOINED_COLUMN`
* 路径 — `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 选定的列 — `Number of customers`

* （输入）按客户存留期收入排名
* [!UICONTROL Column type]： - `Same table > Event Number`
* 事件所有者 — `Number of customers`
* 事件排名 — `Customer's lifetime revenue`
* 筛选器 — `Customer's order number = 1`

* 客户的收入百分位数
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `(input) Ranking by customer lifetime revenue`，`Number of customers`
* [!UICONTROL Calculation]： - **当A为null时为null，否则为null (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]： - `Decimal`

>[!NOTE]
>
>使用的百分位数甚至是客户分段，表示客户群的第X个百分位数。 每个客户都与1到100之间的整数关联，可以将其视为其生命周期收入&#x200B;*排名*。 例如，如果特定客户的收入百分位数为&#x200B;**5**，则该客户在生命周期收入方面位于所有客户的&#x200B;***第五个百分位***。

## 量度

* **总客户存留期值**
* 在`customer_entity`表中
* 此量度执行&#x200B;**总和**
* 在`Customer's lifetime revenue`列上
* 按`Customer's first order date`时间戳排序

## 报告

* **客户集中度**
* [!UICONTROL Metric]： `Total customer lifetime value`
* [!UICONTROL Filter]： `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]： `Total customer lifetime value`
* [!UICONTROL Filter]： `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL 分组依据]: `Independent`
* 量度`A`： `Total customer lifetime revenue by percentile`
* 量度`B`： `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Customer's revenue percentile`
* 显示顶端/底端： `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **前10%浓度**
* [!UICONTROL Filter]： `Customer's revenue percentile <= 10`

* 量度`A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隐藏图表
* &#x200B;
  [!UICONTROL 分组依据]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **仅购买一次的前50%的集中度**

* 量度`A`： `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]：

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隐藏图表
* &#x200B;
  [!UICONTROL 分组依据]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **最低的10%浓度**
* [!UICONTROL Filter]： `Customer's revenue percentile > 90`

* 量度`A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隐藏图表
* &#x200B;
  [!UICONTROL 分组依据]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于上面的示例仪表板。

如果您在构建此分析时遇到任何问题，或只是想与专业服务团队接洽，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)。
