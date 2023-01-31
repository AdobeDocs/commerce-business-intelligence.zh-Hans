---
title: 创建计算列
description: 了解如何整合来自不同来源的数据。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 创建计算列

在分析数据时，整合来自不同来源的数据会很有帮助。 是否要按客户获取来源、关联订单表和Google Analytics的数据对收入进行分组？ 或者，如何按客户性别对收入进行分组，或将客户属性加入交易数据以进行分段？

本指南将教您如何做到这一点。 在开始之前，我们建议您查看 [Calculated Column Types指南](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 的 _Calculated Column Types指南_ 概述可在Data warehouse管理器中创建的列类型及其定义和示例。

1. 要开始配置，请单击 **[!DNL Manage Data > Data Warehouse]** 中。

1. 单击要在中创建列的表。 例如，如果我们想要创建 `Customer Gender` 列中，我们将选择 `sales_flat_order` 表。

1. 将显示表格方案。 单击 **[!UICONTROL Create New Column]**.

1. 为列指定名称 — 例如， `Customer Gender`.

1. 选择列的定义。 这是 [Calculated Column Types指南](../data-warehouse-mgr/calc-column-types.md) 会派上用场的！

1. 对于某些类型的列，需要提供更多信息才能正确创建列：
   * 对于 `One to Many` （已加入）和 `Many to One` （聚合）列，您需要选择表和列。
   * 对于 `Same Table calculation`，则需要从下拉菜单中选择所需的日期字段。

如果您要创建 `One to Many` （连接）或 `Many to One` （聚合）列，您需要选择一个路径来连接两个表。 在此步骤中，您可以使用现有路径或创建新路径。

>[!NOTE]
>
>请记住将表正确定义为多个或一个！

* 如果需要，可以应用 [过滤器](../../data-user/reports/ess-manage-data-filters.md) 到新列。
* 完成后，单击 **[!UICONTROL Save]**.

就这样！ 您的新列将显示在当前表格中，并且 `Pending` 状态。 下次更新完成后，您的列将可用于量度和报表。

## 方便的参考图 {#map}

如果您在创建计算列时记住所有输入内容时遇到问题，请在构建时尽量保持此参考映射方便：

![](../../assets/Calculated_Columns_Example.png)

## 相关文档

* [计算列类型](../data-warehouse-mgr/calc-column-types.md)
* [高级计算列类型](../data-warehouse-mgr/adv-calc-columns.md)
* [建筑 [!DNL Google ECommerce] 包含订单和客户数据的维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
