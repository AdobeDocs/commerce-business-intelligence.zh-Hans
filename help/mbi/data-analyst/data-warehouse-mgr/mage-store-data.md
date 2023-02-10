---
title: 在商务中存储数据
description: 了解数据的生成方式、新行插入其中一个核心商务表的确切原因，以及购买或创建帐户等操作如何记录到商务数据库中。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 3%

---

# 将数据存储在 [!DNL Adobe Commerce]

Adobe Commerce平台记录并组织了数百个表中各种有价值的商务数据。 在本主题中，您将了解如何生成该数据，以及具体导致在 [核心商务表](../data-warehouse-mgr/common-mage-tables.md)，以及购买或创建帐户等操作如何记录到商务数据库中。 要解释这些概念，请参阅以下示例：

`Clothes4U` 是一家既在线又在实体店的服装零售商。 它使用网站后面的Magento Open Source来收集和组织数据。

## `catalog\_product\_entity`

现在是9月22日，而且 `Clothes4U` 正在向其秋季行中推出三个新项目： `Throwback Bellbottoms`, `Straight Leg Jeans`和 `V-Neck T-Shirts`. A `Clothes4U` 员工打开其商务管理员，单击 **[!UICONTROL Add Product]**，并输入 `Throwback Bellbottoms`.

对 `Throwback Bellbottoms`，员工单击 **[!UICONTROL Save]**，在 `catalog_product_entity` 表。 员工重复该过程，为创建另一个新的商务产品 `Straight Leg Jeans`，然后是第三个 `V-Neck T-Shirt`，在 `catalog_product_entity` 表：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — 这是 `catalog_product_entity` 表，表示表的每一行必须具有不同的 `entity_id`. 每个 `entity_id` 此表中只能与一个产品关联，而每个产品只能与一个产品关联 `entity_id`
   * 上表的顶行， `entity_id` = 205，是为“回退贝尔底”创建的新行。 随处 `entity_id` = 205显示在商务平台中，它将引用产品“Throwback Bellbotts”
* `entity_type_id`  — 商务具有多个类别的对象（如客户、地址和产品等），此列用于表示此特定行所属的类别。
   * 这是 `catalog_product_entity` 表中，每行具有相同的实体类型：产品。 在Adobe Commerce, `entity_type_id` 对于产品，为4，这就是为什么创建的所有三个新产品都返回4作为此列的原因。
* `attribute_set_id`  — 属性集用于标识具有相同描述符的产品。
   * 表格的前两行是 `Throwback Bellbottoms` 和 `Straight Leg Jeans` 产品，都是裤子。 这些产品将具有相同的描述符（例如，名称、缝隙、腰围），因此具有相同的描述符 `attribute_set_id`. 第三项， `V-Neck T-Shirt` 有不同的 `attribute_set_id` 因为它没有与裤子相同的描述符；衬衫没有马甲或内裤。
* `sku`  — 这些是用户在Adobe Commerce中创建新产品时分配给每个产品的唯一值。
* `created_at`  — 此列返回创建每个产品的时间戳

## `customer\_entity`

新增三款产品后不久，新客户， `Sammy Customer`，访问次数 `Clothes4U`网站首次。 自 `Clothes4U` 不允许来宾订单， `Sammy Customer` 必须先在网站上创建帐户。 她输入凭据并单击提交，从而在 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 就像前面的表格， `entity_id` 是 `customer_entity` 表。
   * When `Sammy Customer` 创建了她的帐户，上面的一行写到了 `customer_entity` 表格，她被指派了 `entity_id` = 214。 在所有表中，客户均被标识为 `entity_id` = 214将始终指Sammy客户
* `entity_type_id`  — 此列标识此表中列出的实体类型，其功能与 `catalog_product_entity` 表
   * 在 `customer_entity` 表将是客户，而Commerce将客户定义为 `entity_type_id` 默认为1
* `email`  — 此字段由新客户在进行帐户时输入的电子邮件填充
* `created_at`  — 此列返回每个用户加入时的时间戳

## `sales\_flat\_order (or Sales\_order` 如果您拥有Commerce 2.0或更高版本)

她的帐户创建完成后， `Sammy Customer` 准备开始购买。 在浏览网站时，她添加了两对 `Throwback Bellbottoms` 一个 `V-Neck T-Shirt` 到她的车上。 她对自己的选择感到满意，于是开始结帐并提交订单，在 [销售平面订单表](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — 这是 `sales_flat_order` 表。
   * 当Sammy客户下订单时，上面的行写到 `sales_flat_order` 表，则已分配顺序 `entity_id` = 227。
* `customer_id`  — 此列是下达此特定订单的客户的唯一标识符
   * 的 `customer_id` 与此订单相关的是214，这是Sammy客户的 `entity_id` 在 `customer_entity` 表。
* `subtotal`  — 此列是针对订单向客户收取的总金额
   * 这两双“倒背裤”和“V领T恤”总共花了94.85美元
* `created_at`  — 此列返回创建每个订单的时间戳

## `sales\_flat\_order\_item ( or Sales\_order\_item` 如果您拥有Commerce 2.0或更高版本)

除了 `Sales\_flat\_order` 表格，时间 `Sammy Customer` 提交她的顺序，该顺序中每个唯一项目的行将插入到 [`sales\_flat\_order\_item` 表](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — 此列是 `sales_flat_order_item` 表
   * `Sammy Customer`s订单在此表上创建了两行，因为她的订单包含两个不同的产品
* `name`  — 此列是产品的名称
* `product_id`  — 此列是该行所引用产品的唯一标识符
   * 上面的第一行具有 `product_id` = 205，因为 `Throwback Bellbottoms` 拥有 `entity_id` 205年 `catalog_product_entity` 表
* `order_id`  — 此列是 `entity_id` 包含这些特定订单项的订单
   * 上面两行均具有 `order_id` = 227，因为它们都是 `Sammy Customer`, `entity_id` = 227 `sales_flat_order` 表
* `qty_ordered`  — 此列是此特定订单中包含的产品件数
   * `Sammy Customer`s顺序包含2对 `Throwback Bellbottoms`
* `price`  — 此列是订单项目单位的价格
   * 的 `subtotal` 从 `Sammy Customer`的顺序 `sales_flat_order` 表为94.85，即2对的总和 `Throwback Bellbottoms` 39.95美元/1 `V-Neck T-Shirt` 14.95美元。
