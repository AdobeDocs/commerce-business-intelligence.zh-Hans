---
title: 使用日期差异计算列
description: 了解日期差异计算列的用途和用法。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5SElfBoU6vqCNthFdj96eCNH26dC54ucjqknnhQXQy8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 0%

---

# 日期差异计算列

本主题概述了`Date Difference`页面中可用的&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;计算列的用途和用途。 下面是它的作用解释，然后是一个示例，以及创建它的机制。

**解释**

`Date Difference`列类型根据事件时间戳计算属于单个记录的两个事件之间的时间。 此列中计算的原始值以秒为单位，但它会自动转换为分钟、小时、天等，以便在报表中显示。 但是，当用作过滤器/分组时，您希望使用以秒为单位的值。

`date difference`计算列可用于创建计算两个事件之间的平均时间或中间时间的量度，如客户注册和首次订购之间的平均时间。

**示例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


在上述示例中，`Date Difference`列是`Seconds between timestamp_2 and timestamp_1`列。 它执行计算`timestamp_2 minus timestamp_1`。

**机械**

以下步骤描述了如何创建`Date Difference`列。

1. 导航到&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;页面。
1. 导航到要在其上创建此列的表。
1. 单击&#x200B;**[!UICONTROL Create a Column]**&#x200B;并按如下方式配置列：
   * 选择`Column Definition Type` > `Same Table`
   * 选择`Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 选择`Ending DATETIME`列>选择结束日期时间字段，该字段通常是稍后发生的事件
   * 选择`Starting DATETIME`列** >选择开始日期时间字段，该字段通常是较早发生的事件

1. 为列提供一个名称，然后单击&#x200B;**[!UICONTROL Save]**。
1. 该列可立即使用&#x200B;*1}。*

例如，以下示例配置为计算`Seconds between order date and customer's creation date`：

![日期差异计算配置显示日期时间列选择](../../assets/date_diff.png)
