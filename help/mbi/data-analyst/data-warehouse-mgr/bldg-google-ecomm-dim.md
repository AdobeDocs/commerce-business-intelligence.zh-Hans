---
title: 生成[!DNL Google ECommerce] 维度
description: 了解如何构建将您的电子商务数据与您的订单和客户数据关联的维度。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 生成 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

现在您已完成 [连接您的[!DNL Google ECommerce] 帐户](../../data-analyst/importing-data/integrations/google-ecommerce.md)，您可以在中处理这些数据 [!DNL Commerce Intelligence]？ 本主题将指导您构建将电子商务数据与订单和客户数据关联的维度。

所涵盖的维度使您能够构建分析 [回答有关营销渠道和营销活动的重要问题](../../data-analyst/analysis/most-value-source-channel.md). 每个来源占收入的百分比是多少？ 的生命周期值如何 [!DNL Facebook] 已收购客户与来自已收购客户的比较 [!DNL Google]？

## 先决条件和概述

要在此主题中创建维度，您需要 [!DNL Google ECommerce] 表，和 `orders` 表格和a `customers` 表格。 这些表必须 [已同步到您的Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 在生成维度之前。 已同步的表将显示在 `Synced Tables` 的部分 `Data Warehouse Manager`.

如果需要刷新程序，可以快速查看同步表和列：

![](../../assets/Syncing_New_Columns.gif)

从创建连接后 `orders` 表格 [!DNL Google eCommerce] 表，创建下面列表中的前三个维。 接下来，使用这些维度在 `customers` 表格。 最后，将这些列联结到 `orders` 表格。

以下是涉及的维度：

* **订单表**

* 订单的 [!DNL Google Analytics] 源
* 订单的 [!DNL Google Analytics] 中
* 订单的 [!DNL Google Analytics]营销活动
* 客户第一张订单的 [!DNL Google Analytics] 源
* 客户第一张订单的 [!DNL Google Analytics] 中
* 客户第一张订单的 [!DNL Google Analytics] 营销活动

* **Customers表**

* 客户第一张订单的 [!DNL Google Analytics] 源
* 客户第一张订单的 [!DNL Google Analytics] 中
* 客户第一张订单的 [!DNL Google Analytics] 营销活动

## 构建维度

要创建尺寸，请打开 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 通过单击 **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 订单表，第1轮

此示例构建 **订单的 [!DNL Google Analytics] 来源** 维度。

1. 从Data Warehouse中的表列表中，单击该表(在本例中， `orders`)，其中包含您的订单信息。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 选择 `Joined Column` 从 [定义下拉列表](../data-warehouse-mgr/calc-column-types.md). 此示例适用于 [一对一关系](../data-warehouse-mgr/table-relationships.md)，匹配 `eCommerce.transactionID` 一行中的任意一列 `orders` 表格。
1. 接下来，您需要定义路径，或者定义正在使用的表和列的连接方式。 单击 `Select a table and column` 下拉菜单。
1. 您需要的路径不可用，因此需要创建一个新路径。 单击 **[!UICONTROL Create new Path]**.
1. 在显示的窗口中，设置 `Many` 侧到 `orders.order\_id`，或中的列 `orders` 包含订单ID的表。
1. 在 `One` 侧面，查找 `Google ECommerce` 表，然后将列设置为 `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 单击 **[!UICONTROL Save]** 以创建路径。
1. 添加路径后，单击 **[!UICONTROL Select table and column]** 再次下拉菜单。
1. 找到 `ECommerce` 表格，然后单击 `Source` 列。 这会将订单与源信息绑定。
1. 返回表模式后，单击 **[!UICONTROL Save]** 再次创建维度。

下面是整个过程的概况：

![](../../assets/help_center.gif)

接下来，尝试创建 **订单的 [!DNL Google Analytics] 中** 和 `campaign`. 这些维度没有多少变化，所以尝试一下。 但如果你被卡住了，你可以去看看 [本文结尾](#stuck) 看看有什么不同。

### Customers表 {#customers}

此示例构建 **客户第一张订单的 [!DNL Google Analytics] 源** 维度。

1. 从Data Warehouse中的表列表中，单击该表(在本例中， `customers`)，其中包含您的客户信息。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 对于此示例，请选择 `is MAX` 定义 [定义下拉列表](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 此 `is MIN` 如果将定义应用于只有一个可能值的文本列，则该定义也可以正常工作。 重要的部分是确保设置正确的过滤器，您稍后可以这样做。
1. 单击 **[!UICONTROL Select a table and column]** 下拉菜单并选择 `orders` 表，然后 `Order's [!DNL Google Analytics] source` 列。
1. 单击 **[!UICONTROL Save]**.
1. 返回表模式后，单击 `Options` 下拉列表，然后 `Filters`.
1. 单击 **[!UICONTROL Add Filter Set]** 然后选择 `Orders we count` 设置。 您只希望计入您盘点筛选器集的订单中包含的订单，因此选择此筛选器集非常重要。
1. 单击 **[!UICONTROL Add Filter]**. 您要查找客户的第一个订单 [!DNL Google Analytics] 源，因此您需要添加过滤器：

   _orders.Customer的订单号= 1

   _
1. 单击 **[!UICONTROL Save]** 以创建维度。

接下来，尝试创建 **客户第一张订单的 [!DNL Google Analytics] 中** 和 `campaign`. 这些维度没有多少变化，所以尝试一下。 但如果你被卡住了，你可以去看看 [本文结尾](#stuck) 看看有什么不同。

### 奖励：订单表，第2轮

如果需要，可在此处停止，但此部分通过引入 **客户第一张订单的 [!DNL Google Analytics] 维度** 您已在 [最后一节](#customers) 到 `orders` 表格。 在此部分中创建维度可让您分析基于以下项构建的所有量度： `orders` 表 —  `Revenue`， `Number of orders`， `Distinct buyers`，等等 — 使用 [!DNL Google Analytics] 客户第一订单的属性。

此示例将 `Customer's first order's [!DNL Google Analytics] source` 维到 `orders` 表格。

1. 从Data Warehouse中的表列表中，单击该表(在本例中， `orders`)，其中包含您的订单信息。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 选择 `Joined Column` 从“定义”下拉菜单中单击。 这会将您在上一节中创建的客户维加入到 `orders` 表格。
1. 单击 **[!UICONTROL Select a table and column]** 下拉列表，然后选择 `customers` 表格和 `Customer's first order's [!DNL Google Analytics] source` 列。
1. 如果路径未自动填充，请选择最能连接customers和orders表的路径。
1. 单击 **[!UICONTROL Save]** 以创建维度。

下面是整个过程的概况：

![](../../assets/help_center2.gif)

通过加入 `Customer's first order's` 中和 `campaign` 的维度 `orders` 表格。 加入维，如果遇到问题，则检出 [文章的结尾](#stuck) 如果您需要帮助。

### 正在结束

您已完成维度创建，这意味着您现在可以创建强大的分析来跟踪各种渠道和营销活动的性能。 请记住 **新列将不可用，直到下一次更新完成**.

本主题中介绍了一些更受欢迎的维度，但天空才是极限 — 请尝试创建您自己的维度，或者如果您希望获得探索其他选项的帮助，请随时联系我们。 

### 其他说明

**`Orders`表#1**：创建时 `Order's [!DNL Google Analytics]` 中和 `campaign` 维中，差异在于第12步中选择的列。 在此示例中，该列为 `Source`.

**`Customers`表**：创建时 `Customer's first order's [!DNL Google Analytics]` 中和 `campaign` 维中，差异在于第5步中选择的列。 在此示例中，该列为 `Order's [!DNL Google Analytics]` 源。

**`Orders`表#2**：加入时 `Customer's first order's [!DNL Google Analytics]` 中和 `campaign` 列到 `orders` 表，其差异为在第5步中选择的列。 在此示例中，该列为 `Customer's first order's [!DNL Google Analytics]` 源。
