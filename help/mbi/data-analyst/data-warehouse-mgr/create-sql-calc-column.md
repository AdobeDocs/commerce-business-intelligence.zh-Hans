---
title: 创建和使用SQL计算列
description: 了解如何在新的MBI架构上以SQL计算列的形式创建高级列。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 创建SQL计算列

本主题概述 `Calculation` 列类型：可以使用 [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md). 下面说明了SQL计算的用途、使用原因、创建SQL计算的过程，以及两个示例。

**说明**

过去，在 `advanced` 只能由此处的客户成功团队分析师完成 [!DNL MBI]. 现在，所有功能都掌握在最终用户手中，并且高级列可以以 `SQL Calculation` 列 [!DNL MBI] 架构。

的 `Calculation` 列类型(现在作为Data warehouse管理器中的一个选项提供)是一种表操作，它允许您使用PostgreSQL逻辑转换表上的列。 有关可在 `Calculatio`在PostgreSQL网站上可以找到n列类型 [此处](https://www.postgresql.org/docs/9.6/static/functions.html).

可使用 `Calculation` 列几乎是无限的，但大多数列都可以使用IF-THEN语句和基本算术来创建，这些运算将在以下示例中使用。

**示例1:客户的最后订单吗？**

大多数帐户都有一个名为 `Is customer's last order?` 在 `orders` 表格，用于对重复购买率和已弃用的客户进行分析。 如果您的帐户在新架构上，则此列是使用 `Calculation` 列中，可在以下屏幕截图中看到：

![](../../assets/Is_customer_s_last_order.png)

的 `Is customer's last order?` 列使用输入 `Customer's lifetime number of orders` 和 `Customer's order number` 别名为 `A` 和 `B` 分别进行。

逐行显示， PostgreSQL的含义是：

* 用例：这会启动一系列If - Then语句
* when `A` 为null或 `B` 为null，则为null。如果任一输入为空，则输出也应为空。 这是为了防止SQL错误
* when `A=B` then `Yes`:如果 `Customer's lifetime number of orders` 等于 `Customer's order number` 对于此行，返回 `Yes`. 如果客户下了4个订单，则第4个订单的行将返回 `Yes` 表示 `Is customer's last order?`
* else `No`:如果没有其他语句满足，则返回 `No`
* 结束：这会结束If - Then语句

此列可返回的可能值(`NULL`, `Yes`, `No`)包含非数字字符，因此此处的数据类型为字符串。

**示例2:订单物料总值（数量*价格）**

我们的许多客户喜欢在项目级别分析收入，按字段(如 `product name` 或 `category`. 大多数数据库实际上并不会按订单为您提供产品的收入；而是提供订单中的销售数量和物料的价格。

为启用产品收入分析，大多数帐户都有一列，称为 `Order item total value (quantity * price)` 在 `Orders Items` 表。 如果您的帐户在新架构上，则此列也使用 `Calculation` 列中，可在以下屏幕截图中看到：

![](../../assets/Order_item_total_value.png)

在商务架构中， `Order item total value (quantity * price)` 列使用输入 `qty ordered` 和 `base price` 别名为 `A` 和 `B` 分别进行。

此新列将返回的值将为美元和美分，因此正确的数据类型为 `Decimal(10,2)`.

**力学**

新 `Calculation` 列可通过导航到 **[!DNL Manage Data > Data Warehouse]** 如下所示：

![](../../assets/blobid2.png)

从此处，您可以创建新 `Calculation` 列中，请执行以下步骤：

1. 选择要在其上添加 `Calculation` 列。
1. 在正确的表中，单击 **[!UICONTROL Create New Column]** 中。
1. 从 `Select a definition` 下拉列表，选择 `Same Table`.
1. 选择 `Calculation` 作为 `column definition equation`.
1. 输入列名称。
1. 选择 `input` 列。 您添加的每列都将获得字母别名，因此第一列将为 `A`，第二个是 `B` 等等。
1. 在窗口中，使用输入的字母别名键入新列的PostgreSQL逻辑。 SQL计算应限于单个列定义，包括SQL查询的SELECT和FROM语句之间的所有逻辑。 请注意，使用任何输入字母的SQL关键字应为小写。 例如，在使用 `CASE` 语句，应使用小写 —  `case`. 系统假定大写 `A` 是指其中一个输入。
1. 选择相应的数据类型。
   * `Integer`  — 整数
   * `Decimal(10,2)`  — 总数为10位的小数，其中2位于小数点的右侧
   * `String`  — 使用非数字的任何类型的文本或一系列字符
   * `Datetime` - yyyy-MM-dd hh:mm:ss格式

1. 单击 **[!UICONTROL test column]**. 这将为每个输入生成一个包含5个测试值的列表，并针对每组测试值显示步骤6中的逻辑结果。 如果SQL的任何部分生成错误，则将返回相应的错误消息。 请注意，仅当所有输入列都是本机字段时，才能生成示例结果。 如果有任何输入列是计算列，您需要通过将列添加到量度并在可视化Report Builder中查看来验证结果
1. 如果您对结果满意，请单击 **[!UICONTROL Save]**，且您的列将可供使用。
