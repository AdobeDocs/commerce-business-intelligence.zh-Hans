---
title: 在Adobe Commerce中存储数据
description: 了解如何生成数据、导致插入新行的原因以及如何将操作记录到Adobe Commerce数据库中。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# 在[!DNL Adobe Commerce]中存储数据

[!DNL Adobe Commerce]平台记录并整理了数百个表中的各种有价值的商业数据。 本主题介绍：

* 如何生成该数据
* 导致在[核心Commerce表](../data-warehouse-mgr/common-mage-tables.md)之一中插入新行的原因
* 如何将购买或创建帐户等操作记录到[!DNL Adobe Commerce]数据库中

要讨论这些概念，请参阅以下示例：

`Clothes4U`是一个服装retailer，具有在线和实体存在。 它在其网站后使用[!DNL Magento Open Source]来收集和整理数据。

## `catalog\_product\_entity`

现在是9月22日，`Clothes4U`正在向其秋季行推出三个新项目：`Throwback Bellbottoms`、`Straight Leg Jeans`和`V-Neck T-Shirts`。 `Clothes4U`员工打开其Commerce管理员，单击&#x200B;**[!UICONTROL Add Product]**，然后输入`Throwback Bellbottoms`的所有信息。

对`Throwback Bellbottoms`的所有设置感到满意，员工单击&#x200B;**[!UICONTROL Save]**&#x200B;后，这会将第一行插入到`catalog_product_entity`表中。 该员工重复该过程，为`Straight Leg Jeans`创建另一个Commerce产品，然后为`V-Neck T-Shirt`创建第三行，并将以下第二行和第三行插入到`catalog_product_entity`表中：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | 裤子10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | 衬衫6 | 2016/09/22 09:24:02 |

* `entity_id` — 这是`catalog_product_entity`表的主键，这意味着该表的每一行必须具有不同的`entity_id`。 此表上的每个`entity_id`只能与一个产品关联，并且每个产品只能与一个`entity_id`关联
   * 上表的顶行，`entity_id` = 205，是为“Rewback Bellbottoms”创建的新行。 在Commerce平台中出现的`entity_id` = 205处，即指产品“Rewback Bellbottoms”
* `entity_type_id` - Commerce具有多种对象类别（如客户、地址和产品，仅举几例），此列用于表示此特定行所属的类别。
   * 这是`catalog_product_entity`表，每行具有相同的实体类型： product。 在Adobe Commerce中，产品的`entity_type_id`为4，因此创建的全部三个新产品都会为此列返回4。
* `attribute_set_id` — 属性集用于标识描述符相同的产品。
   * 表的前两行是`Throwback Bellbottoms`和`Straight Leg Jeans`产品，它们都是裤子。 这些产品将具有相同的描述符（例如，name、inseam、waisline），因此具有相同的`attribute_set_id`。 第三个项目`V-Neck T-Shirt`具有不同的`attribute_set_id`，因为它没有与裤子相同的描述符；衬衫没有腰围或内衬。
* `sku` — 这些是用户在Adobe Commerce中创建产品时分配给每个产品的唯一值。
* `created_at` — 此列返回每个产品的创建时间戳

## `customer\_entity`

在添加三个新产品后不久，新客户`Sammy Customer`首次访问`Clothes4U`的网站。 由于`Clothes4U`不允许来宾订单，因此`Sammy Customer`必须首先在网站上创建帐户。 客户输入所需的凭据并单击“提交”，在[`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)上生成以下新条目：

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` — 与上一个表一样，`entity_id`是`customer_entity`表的主键。
   * 当`Sammy Customer`创建帐户并将上述行写入`customer_entity`表时，为客户分配了`entity_id` = 214。 在所有表中，标识为`entity_id` = 214的客户始终引用用户Sammy Customer
* `entity_type_id` — 此列标识此表中列出的实体类型，其功能与在`catalog_product_entity`表中相同
   * `customer_entity`表中的每一行都是客户，Commerce默认将客户定义为`entity_type_id` 1
* `email` — 此字段由新客户在创建其帐户时输入的电子邮件填充
* `created_at` — 此列返回每个用户加入时的时间戳

## 如果您有`sales\_flat\_order (or Sales\_order`，则为[!DNL Adobe Commerce 2.x]

帐户创建完成后，`Sammy Customer`可以开始购买。 在网站上，客户将两对`Throwback Bellbottoms`和一对`V-Neck T-Shirt`添加到购物车。 客户对选择感到满意，将移至结帐并提交订单，并在[销售平面订单表](../data-warehouse-mgr/sales-flat-order-table.md)上创建以下条目：

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` — 这是`sales_flat_order`表的主键。
   * 当Sammy客户下达此订单并将上述行写入`sales_flat_order`表时，已分配该订单`entity_id` = 227。
* `customer_id` — 此列是下此特定订单的客户的唯一标识符
   * 与此订单关联的`customer_id`是214，它是`entity_id`表中Sammy客户的`customer_entity`。
* `subtotal` — 此列是该订单向客户收取的总金额
   * 两双“Rewback Bellbottoms”和“V领T恤”总共花费94.85美元
* `created_at` — 此列返回创建每个订单的时间戳

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(如果您使用的是Commerce 2.0或更高版本)

除了`Sales\_flat\_order`表上的单行外，当`Sammy Customer`提交订单时，该订单中每个唯一项的一行将插入到[`sales\_flat\_order\_item`表](../data-warehouse-mgr/sales-flat-order-item-table.md)中：

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` — 此列是`sales_flat_order_item`表的主键
   * `Sammy Customer`的订单在此表中创建了两个行，因为该订单包含两个不同的产品
* `name` — 此列是产品的名称
* `product_id` — 此列是该行所引用产品的唯一标识符
   * 上面第一行的`product_id` = 205，因为`Throwback Bellbottoms`在`entity_id`表上有`catalog_product_entity`，即205
* `order_id` — 此列是包含这些特定订单项的订单的`entity_id`
   * 上面两行都具有`order_id` = 227，因为它们都是`Sammy Customer`下达的订单的一部分，该订单在`entity_id`表中具有`sales_flat_order` = 227
* `qty_ordered` — 此列是此特定订单中包含的产品件数
   * `Sammy Customer`的订单包含两对`Throwback Bellbottoms`
* `price` — 此列是订单项目的单件价格
   * `subtotal`表中`Sammy Customer`顺序中的`sales_flat_order`为94.85，即`Throwback Bellbottoms`对（每对$39.95）和1 `V-Neck T-Shirt`对(14.95$14.95)的总和。
