---
title: 合并表
description: 了解如何整合表和数据库。
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 合并表

如果您在多个商店前线或市场中进行操作，则可能会单独存储类似的数据库。 在[!DNL Adobe Commerce Intelligence]中，将不同数据库中的相似表合并到一起很容易。

例如，您可能有针对`orders`的`Market A`表以及针对`orders`的类似`Market B`表。 [!DNL Commerce Intelligence]可以合并两个表，并允许您查看来自`Market A`和`B`的汇总订单数据，以及按特定市场进行分段。

若要合并表，输入表必须具有&#x200B;**相似的结构**。 换言之，所有输入表都必须包含统一表中所需的数据列。

本主题讨论统一表的一些最常见用例以及创建自己的统一表所需的后续步骤。

## 关于何时使用统一表的建议

下面讨论在系统中使用统一表的适当时机。

### 集成来自多个网站的数据

如果您在不同品牌和网站下销售产品，则每个品牌或网站的表格结构可能类似。

例如，您可能有网站`orders`的`A`表和网站`orders`的单独但类似的`B`表。 在这种情况下，合并网站`orders`和`A`中的`B`表可能很有用。 这样，除了能够按网站`A`和`B`划分量度外，您还可以查看这两个网站的合并收入和订单数。

### 集成旧版数据

许多公司都曾经重构过数据库，而旧数据库中的数据并不总是能够转换为新系统。 您可以使用统一表将旧式表中的键列与活动系统中的键列连接起来。 这允许您在整个历史过程中对数据进行统一分析。

### 组合活动用户分析事件

想象一下，在一个网站上，用户可以做多种事情：参加调查、玩游戏、购物、介绍朋友等等。 通常，这些事件中的每一个都存储在其自己的表中。 这使得难以分析在给定时间段内有多少不同的用户至少采取了任何类型的行动。

您可以使用统一表创建一个包含所有用户以及发生其中任何事件的统一列表。 然后，可以对统一表运行查询以轻松进行此类分析。

与Data Warehouse中的所有其他表一样，您可以添加其他列来支持各种图表和分析。

## 创建、查看或更新统一表

如果您有兴趣将统一表添加到Data Warehouse，请联系[!DNL Commerce Intelligence] [支持](../guide-overview.md#Submitting-a-Support-Ticket)。

>[!NOTE]
>
>由于统一表在`Data Warehouse Manager`中不可查看，因此只能由[!DNL Commerce Intelligence]支持人员查看和更新这些表。
