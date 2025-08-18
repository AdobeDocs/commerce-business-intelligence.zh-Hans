---
title: 创建计算列
description: 了解如何合并来自不同来源的数据。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 创建计算列

在分析数据时，整合来自不同来源的数据会很有帮助。 要按客户获取来源对收入进行分组，并关联`orders`表中的数据和[!DNL Google Analytics]数据？ 您可能需要按客户性别对收入进行分组，或将客户属性加入交易数据以进行分段。 本主题将讨论如何做到这一点。

在开始使用之前，Adobe建议您查看[计算列类型指南](../../data-analyst/data-warehouse-mgr/calc-column-types.md)，以了解有关您可以在Data Warehouse Manager中创建的列类型的信息，以及它们的定义和示例。

1. 若要开始，请单击&#x200B;**[!DNL Manage Data > Data Warehouse]**。

1. 单击要在其中创建列的表。 例如，如果要为收入分段创建一个`Customer Gender`列，则可以选择`sales_flat_order`表。

1. 此时将显示表方案。 单击&#x200B;**[!UICONTROL Create New Column]**。

1. 为您的列提供一个名称。 例如，`Customer Gender`。

1. 选择列的定义。 这是[计算列类型指南](../data-warehouse-mgr/calc-column-types.md)的方便之处！

1. 对于某些类型的列，需要更多信息才能正确创建列：

   * 对于`One to Many` （已联接）和`Many to One` （聚合）列，您需要选择表和列。

   * 对于`Same Table calculation`，您需要从下拉列表中选择所需的日期字段。

如果要创建`One to Many`（已联接）或`Many to One`（聚合）列，则需要选择路径以连接两个表。 在此步骤中，您可以使用现有路径或创建路径。

>[!NOTE]
>
>请记得将表正确定义为多个表或一个表！

* 如果需要，您可以将[筛选器](../../data-user/reports/ess-manage-data-filters.md)应用到新列。

* 完成后，单击&#x200B;**[!UICONTROL Save]**。

您的新列显示在当前表中，状态为`Pending`。 在下一次更新完成后，您的列将可用于量度和报表。

## 方便的参考地图 {#map}

如果您在创建计算列时无法记住所有输入，请尝试在构建时方便使用此参考图：

![](../../assets/Calculated_Columns_Example.png)

## 相关文档

* [计算列类型](../data-warehouse-mgr/calc-column-types.md)
* [高级计算列类型](../data-warehouse-mgr/adv-calc-columns.md)
* [使用订单和客户数据生成 [!DNL Google ECommerce] 维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
