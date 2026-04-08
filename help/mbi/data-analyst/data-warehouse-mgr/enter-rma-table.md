---
title: enterprise_rma表
description: 了解如何分析有关特定退货请求的信息。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: ad4dda927f0b1b2eba9596d7adfd1419676cf03d
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# enterprise_rma表

`enterprise_rma`表（在Adobe Commerce 2.x中通常称为`magento_rma`，但可以自定义名称）中的每一行都包含有关特定回访请求的信息。

>[!NOTE]
>
>仅当您是`Enterprise Edition`或`Enterprise Cloud Edition`客户时，此表格才包含在您的Adobe Commerce帐户中。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `entity_id` | 表的唯一标识符。 每个`entity_id`表示一个返回请求。 |
| `date_requested` | 请求返回的日期。 |
| `status` | 返回的状态。 值包括“received”、“pending”、“authorized”等。 |
| `order_id` | 与`sales_flat_order`表关联的外键。 |
| `customer_id` | 与`customer_entity`表关联的外键。 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Order's created_at` | 这是原始订单的日期。 这可用于获取订单与退货请求之间的间隔时间。 |
| `Customer's order number` | 这是与原始订单关联的客户订单编号。 |
| `Seconds between order's created_at and return's date_requested` | 从订单日期到退货请求的秒数。 |
| `Return's total value` | 这是返回的总货币金额。 这是每个退货项目的单独退货金额的总和。 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of returns` | 请求的返回次数。 | `Operation`列：`entity_id`<br>`Operation`：`Count`<br>`Timestamp`列：`date requested` |
| `Total returned amount` | 返回的货币总金额。 | `Operation `列：`Return's total value`<br>`Operation`： Sum<br>`Timestamp`列：请求的日期 |
| `Average returned amount` | 平均退货货币金额。 | `Operation`` Column: Return's total value`<br>`Operation`： `Average`<br>`Timestamp`列： `date requested` |
| `Average time to return` | 从订单到退货的平均时间。 | `Operation`列：订单创建日期与请求返回日期之间的秒数<br>`Operation`： `Average`<br>`Timestamp`列： `date requested` |

{style="table-layout:auto"}

## 与其他表的连接

`sale_flat_order`

* 创建联接列，以通过下列联接在`enterprise_rma`表中按订单级属性进行分段和筛选：
   * Commerce 1.x： `enterprise_rma.order_id` （多个） => `sales_flat_order.entity_id` （一个）
   * Commerce 2.x： `magento_rma.order_id` （多个）=> `sales_order.entity_id` （一个）

`enterprise_rma_item_entity`

* 通过以下连接在`Return's total value`表上创建多对一列，例如`enterprise_rma`：
   * Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id` （多个） => `enterprise_rma.entity_id` （一个）
   * Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （多个）=> `magento_rma.entity_id` （一个）
