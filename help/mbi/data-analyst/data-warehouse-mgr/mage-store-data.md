---
title: 在Adobe Commerce中存储数据
description: 了解如何生成数据、导致插入新行的原因以及如何将操作记录到Adobe Commerce数据库中。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# 将数据存储在 [!DNL Adobe Commerce]

此 [!DNL Adobe Commerce] platform可以跨数百个表记录并组织各种有价值的商业数据。 本主题介绍以下内容：

* 如何生成该数据
* 导致新行插入其中一行的原因 [核心Commerce表](../data-warehouse-mgr/common-mage-tables.md)
* 如何将操作（如购买或创建帐户）记录到 [!DNL Adobe Commerce] 数据库

要讨论这些概念，请参阅以下示例：

`Clothes4U` 是一家服装零售商，既有在线业务，也有实体业务。 它使用 [!DNL Magento Open Source] 在其网站后收集并组织数据。

## `catalog\_product\_entity`

现在是9月22日， `Clothes4U` 将在秋季生产线上推出三项新产品： `Throwback Bellbottoms`， `Straight Leg Jeans`、和 `V-Neck T-Shirts`. A `Clothes4U` 员工打开其Commerce管理员，单击 **[!UICONTROL Add Product]**，并输入的所有信息 `Throwback Bellbottoms`.

满意以下项的所有设置 `Throwback Bellbottoms`，员工点击量 **[!UICONTROL Save]**，这会将下面的第一行插入到 `catalog_product_entity` 表格。 员工重复该过程，为创建另一个Commerce产品 `Straight Leg Jeans`，第三个用于 `V-Neck T-Shirt`，将下面的第二行和第三行插入到 `catalog_product_entity` 表：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — 这是 `catalog_product_entity` 表，表示表的每一行必须具有不同的 `entity_id`. 每个 `entity_id` 此表只能与一个产品关联，每个产品只能与一个产品关联 `entity_id`
   * 上表的顶行， `entity_id` = 205，是为“Rewback Bellbottoms”创建的新行。 任何位置 `entity_id` = 205显示在Commerce平台中，它是指产品“Rewback Bellbottoms”
* `entity_type_id` - Commerce有多个对象类别（如客户、地址和产品，这里只列举几个），此列用于表示此特定行所属的类别。
   * 这就是 `catalog_product_entity` 表，每行具有相同的实体类型：product。 在Adobe Commerce中， `entity_type_id` for product为4，因此创建的全部三个新产品都会返回此列的4。
* `attribute_set_id`  — 属性集用于标识具有相同描述符的产品。
   * 表的前两行是 `Throwback Bellbottoms` 和 `Straight Leg Jeans` 产品，都是裤子。 这些产品将具有相同的描述符（例如，名称、嵌入、腰围），因此具有相同的描述符 `attribute_set_id`. 第三个项目， `V-Neck T-Shirt` 有不同的 `attribute_set_id` 因为它不会像裤子那样有描述者，衬衫没有腰围或衬衫。
* `sku`  — 这些是用户在Adobe Commerce中创建产品时分配给每个产品的唯一值。
* `created_at`  — 此列返回每个产品创建时间的时间戳

## `customer\_entity`

在添加三个新产品后不久，新客户 `Sammy Customer`，访问次数 `Clothes4U`第一次访问网站。 从 `Clothes4U` 不允许客人下单， `Sammy Customer` 必须先在网站上创建帐户。 客户输入所需的凭据并单击“提交”，在 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)：

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 和前一张桌子一样 `entity_id` 是的主键 `customer_entity` 表格。
   * 时间 `Sammy Customer` 创建了一个帐户，并且上面的一行被写入 `customer_entity` 表，客户已分配 `entity_id` = 214. 在所有表中，客户标识为 `entity_id` = 214始终指用户Sammy Customer
* `entity_type_id`  — 此列标识此表中列出的实体类型，其作用与它在 `catalog_product_entity` 表
   * 上的每一行 `customer_entity` 表是客户，而Commerce将客户定义为 `entity_type_id` 默认为1
* `email`  — 此字段由新客户在生成帐户时输入的电子邮件填充
* `created_at`  — 此列返回每个用户加入时的时间戳

## `sales\_flat\_order (or Sales\_order` 如果您拥有 [!DNL Adobe Commerce 2.x]

帐户创建完成后， `Sammy Customer` 已准备好开始购买。 在网站上，客户添加了两对的 `Throwback Bellbottoms` 和一个 `V-Neck T-Shirt` 到购物车。 对选择满意，客户移至结帐处并提交订单，并在以下页面上创建以下条目 [销售统一订单表](../data-warehouse-mgr/sales-flat-order-table.md)：

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — 这是 `sales_flat_order` 表格。
   * 当Sammy Customer下此订单，并且上面行被写入 `sales_flat_order` 表，已分配顺序 `entity_id` = 227.
* `customer_id`  — 此列是下此特定订单的客户的唯一标识符
   * 此 `customer_id` 与此订单关联的214是Sammy客户的 `entity_id` 在 `customer_entity` 表格。
* `subtotal`  — 此列是订单中向客户收取的总金额
   * 两款“Rewback Bellbottoms”和“V领T恤”总共售价94.85美元
* `created_at`  — 此列返回创建每个订单的时间戳

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（如果您使用的是Commerce 2.0或更高版本）

除了 `Sales\_flat\_order` 表，时间 `Sammy Customer` 提交订单，该订单中每个唯一项目都有一行插入到 [`sales\_flat\_order\_item` 表](../data-warehouse-mgr/sales-flat-order-item-table.md)：

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — 此列是 `sales_flat_order_item` 表
   * `Sammy Customer`的订单在此表中创建了两个行，因为订单包含两个不同的产品
* `name`  — 此列是产品的名称
* `product_id`  — 此列是该行所引用产品的唯一标识符
   * 上面第一行具有 `product_id` = 205，因为 `Throwback Bellbottoms` 有一个 `entity_id` 205的 `catalog_product_entity` 表
* `order_id`  — 此列是 `entity_id` 包含这些特定订单项的订单的编号
   * 上面两行都具有 `order_id` = 227，因为它们都是由下订单的一部分 `Sammy Customer`，具有 `entity_id` = 227 on the `sales_flat_order` 表
* `qty_ordered`  — 此列是此特定订单中包含的产品单位数
   * `Sammy Customer`的订单包含两对 `Throwback Bellbottoms`
* `price`  — 此列是订单项目的单件价格
   * 此 `subtotal` 起始日期 `Sammy Customer`的订单 `sales_flat_order` 表是94.85，是两对的总和 `Throwback Bellbottoms` 39.95美元，和1美元 `V-Neck T-Shirt` 14.95美元。
