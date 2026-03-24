---
title: 实体关系图
description: 了解一些ER图，以帮助您可视化少数几个通用Commerce数据库表之间的关系。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/pWd5aVoaq2TPkGr37cNeF8CEZ63fItwCEez61eEgGBo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 346
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

![实体关系图，显示从sales_flat_order到customer_entity的路径](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

一个订单可以包含许多项目。 这两个表之间的关系是`sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`。

在[!DNL Commerce Intelligence]内，如果这两个表之间的路径不存在，您可以[在Data Warehouse选项卡中创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)。 准备创建路径时，请如下所示定义路径。

![实体关系图，显示从sales_flat_order_item到sales_flat_order](../../assets/SFOI___SFO_path.png)的路径

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

一个产品可以购买多个项目。 这两个表之间的关系是`catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`。

在[!DNL Commerce Intelligence]内，如果这两个表之间的路径不存在，您可以[在Data Warehouse选项卡中创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)。 准备创建路径时，请如下所示定义路径。

![实体关系图，显示从sales_flat_order_item到catalog_product_entity的路径](../../assets/SFOI___CPE_path.png)
