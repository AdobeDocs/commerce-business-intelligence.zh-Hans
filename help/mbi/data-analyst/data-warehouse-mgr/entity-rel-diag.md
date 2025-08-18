---
title: 实体关系图
description: 了解一些ER图，以帮助您可视化少数几个通用Commerce数据库表之间的关系。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 实体关系图

什么是&#x200B;**[!UICONTROL entity relationship (ER) diagram]**？ [!UICONTROL ER]图是数据库中表及其相互关系的可视化图表。 本主题包含一些[!UICONTROL ER]关系图，可帮助您可视化一些常见的Adobe Commerce数据库表之间的关系。

>[!NOTE]
>
>在整个主题中，您都看到单词&#x200B;**加入**、**关系**&#x200B;和&#x200B;**路径**。 这些词都用于描述两个表如何连接。

## 核心Commerce [!UICONTROL ER]关系图

![4_DB_Chart](../../assets/4_DB_Chart.png)

此`ER`图表示Commerce数据库中核心表之间的关系。 通过一次查看多个关系，您可以看到数据在多个表中的关系。

以下部分包含一次两个表特定的`ER`个图。 要查看图表及其随附的说明，请单击该部分的标题。

## `customer\_entity & sales\_flat\_order`

![一个客户多个订单](../../assets/2_OneCustomerManyOrders.png)

一个客户可以下很多订单。 这两个表之间的关系是`customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id`不等于`sales\_flat\_order.entity\_id`。 第一个可以视为`customer\_id`，第二个可以视为`order\_id.`

在[!DNL Commerce Intelligence]内，如果这两个表之间的路径不存在，您可以[在Data Warehouse选项卡中创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)。 当您准备好创建路径时，其定义如下：

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

一个订单可以包含许多项目。 这两个表之间的关系是`sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`。

在[!DNL Commerce Intelligence]内，如果这两个表之间的路径不存在，您可以[在Data Warehouse选项卡中创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)。 准备创建路径时，请如下所示定义路径。

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

一个产品可以购买多个项目。 这两个表之间的关系是`catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`。

在[!DNL Commerce Intelligence]内，如果这两个表之间的路径不存在，您可以[在Data Warehouse选项卡中创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)。 准备创建路径时，请如下所示定义路径。

![](../../assets/SFOI___CPE_path.png)
