---
title: 创建和使用SQL计算列
description: 了解如何在新的Adobe Commerce Intelligence架构上以SQL计算列的形式创建高级列。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# 创建SQL计算列

本主题概述了 `Calculation` 列类型，可使用将其添加到表中 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md). 下面说明了SQL计算的用途、使用它们的原因、创建SQL计算的过程以及两个示例。

**说明**

过去，被视为 `advanced` 只能由位于此处的客户成功团队的分析师完成 [!DNL Adobe Commerce Intelligence]. 现在，所有权力都掌握在最终用户手中，高级列可以以下列形式创建 `SQL Calculation` 列与新 [!DNL Commerce Intelligence] 架构。

此 `Calculation` 列类型现在作为Data Warehouse管理器中的一个选项提供，它是一种表操作，允许您使用PostgreSQL逻辑转换表上的列。 有关中可用的函数和运算符的文档 `Calculation` 列类型可在PostgreSQL网站上找到 [此处](https://www.postgresql.org/docs/9.6/functions.html).

可以使用创建的不同列 `Calculation` 列几乎是无限的，但大多数列都可以使用IF-THEN语句和基本算术来创建，具体如下例所示。

**示例1：是客户的最后一个订单？**

大多数帐户都有一个名为 `Is customer's last order?` 在他们的 `orders` 此表用于分析重复购买率和客户流失。 如果您的帐户位于新架构上，则此列是使用 `Calculation` 列中，并可在以下屏幕快照中看到：

![](../../assets/Is_customer_s_last_order.png)

此 `Is customer's last order?` 列使用输入 `Customer's lifetime number of orders` 和 `Customer's order number` 别名为 `A` 和 `B` 的量度。

逐行，PostgreSQL的含义是：

* 用例：这将启动一系列If - Then语句
* 时间 `A` 为null或 `B` Is null然后null：如果任一输入为空，则输出也应为空。 这是为了防止SQL错误
* 时间 `A=B` 则 `Yes`：如果 `Customer's lifetime number of orders` 等于 `Customer's order number` 对于此行，则返回 `Yes`. 因此，如果客户已下达了四份订单，则其第四份订单的行将返回 `Yes` 对象 `Is customer's last order?`
* 否则 `No`：如果满足语句时没有其他语句，则返回 `No`
* end：这将结束If - Then语句

此列可以返回的可能值(`NULL`， `Yes`， `No`)包含非数字字符，因此此处的数据类型为字符串。

**实例2：订单项目合计值（数量x价格）**

许多客户喜欢在项目级别分析收入，并按字段（如）进行分片 `product name` 或 `category`. 大多数数据库实际上并不提供订单中产品的收入；而是提供订单中销售的数量和项目的价格。

要启用产品收入分析，大多数帐户都有一个名为的列 `Order item total value (quantity * price)` 在他们的 `Orders Items` 表格。 如果您的帐户位于新架构上，则还会使用 `Calculation` 列中，并可在以下屏幕快照中看到：

![](../../assets/Order_item_total_value.png)

在Commerce架构中， `Order item total value (quantity * price)` 列使用输入 `qty ordered` 和 `base price` 别名为 `A` 和 `B` 的量度。

此新列返回的值以美元和美分表示，因此正确的数据类型为 `Decimal(10,2)`.

**力学**

新 `Calculation` 列可以通过导航到 **[!DNL Manage Data > Data Warehouse]** 如下所示：

![](../../assets/blobid2.png)

从此处，您可以创建 `Calculation` 列按以下步骤操作：

1. 选择要在其上添加 `Calculation` 列。
1. 在正确的表格上时，单击 **[!UICONTROL Create New Column]** 在屏幕的右上角。
1. 从 `Select a definition` 下拉列表，选择 `Same Table`.
1. 选择 `Calculation` 作为 `column definition equation`.
1. 输入列名。
1. 选择 `input` 表中在新列的逻辑中使用的列。 您添加的每一列都有一个字母别名，因此第一列为 `A`，其次是 `B` 等等。
1. 在窗口中，使用输入的字母别名键入新列的PostgreSQL逻辑。 SQL计算应限于单个列定义，包括SQL查询的SELECT和FROM语句之间的所有逻辑。 使用任何输入字母的SQL关键字都应使用小写。 例如，使用 `CASE` 语句中，它应该用小写字母书写 —  `case`. 系统假定大写 `A` 是指输入内容之一。
1. 选择适当的数据类型。
   * `Integer`  — 整数
   * `Decimal(10,2)`  — 总位数为10的小数，其中2位在小数点的右侧
   * `String`  — 使用非数字的任意文本类型或字符系列
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` 格式

1. 单击 **[!UICONTROL test column]**. 这会为每个输入生成一个包含五个测试值的列表，并显示步骤6中针对每组测试值的逻辑结果。 如果SQL的任何部分生成错误，则会返回相应的错误消息。 仅当所有输入列都是本地字段时，才能生成示例结果。 如果有任何输入列是计算列，则必须通过将该列添加到指标并在可视化Report Builder中查看来验证结果

1. 如果对结果满意，请单击 **[!UICONTROL Save]**. 列允许使用。
