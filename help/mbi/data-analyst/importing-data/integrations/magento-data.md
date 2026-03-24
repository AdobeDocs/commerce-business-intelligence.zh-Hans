---
title: 预期Commerce数据
description: 浏览Commerce用户导入Commerce Intelligence的主要数据表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
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
source-wordcount: 239
ht-degree: 0%

---

# 预期[!DNL Adobe Commerce]数据

在您[连接 [!DNL Adobe Commerce] 存储区](../../../data-analyst/importing-data/integrations/magento.md)后，您可以使用Data Warehouse Manager轻松地跟踪Commerce数据库中的相关数据字段以供分析。

本主题探讨Commerce用户导入到[!DNL Commerce Intelligence]中的主要数据表。

| **表名** | **描述** |
|-----|-----|
| `Customers` | `customer\_entity`和相关表描述了与数据库中的每个&#x200B;*注册客户*&#x200B;相关联的信息，如其电子邮件地址和注册日期。 利用这些信息，您可以开始按客户级别的属性和同类群组进行分段。 |
| `Orders` | `sales\_flat\_order`表记录所有订单，包括发出订单的`created\_at`时间戳和汇总收入的`base\_grand\_total`字段。 这些字段是订单级别量度的基础。 如果订单是由&#x200B;*注册客户*&#x200B;发出的，`customer\_id`字段将链接回`customer\_entity`表，以便分析客户的购买行为。 |
| `Order items` | `sales\_flat\_order\_item`表记录每个属于订单的项目。 这包括`price`和`qty\_ordered`字段以及连接到`order\_id`表的`sales\_flat\_order`字段。 此表是`Item sold`等量度的基础，允许您按`product`和`product type`进行分段。 |
| `Products` | `catalog\_product\_entity`表存储有关产品级属性的信息，如类别、大小和颜色。 |
| `Categories` | 您的产品属于一个或多个不同的`product categories`，具体取决于您的Commerce内部版本的设置方式。 `catalog\_category\_entity`表存储这些类别的层次结构（例如，服装>上衣> T恤），`catalog\_category\_product`表记录您的产品与这些类别之间的连接。 |

{style="table-layout:auto"}

## 相关

* [正在连接 [!DNL Adobe Commerce]](../integrations/magento.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
