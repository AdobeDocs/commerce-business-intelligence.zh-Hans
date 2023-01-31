---
title: 生成[!DNL Google ECommerce]维度
description: 了解如何构建维度，以将您的电子商务数据与订单和客户数据关联起来。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# 生成 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

现在你完成了 [连接[!DNL Google ECommerce]帐户](../../data-analyst/importing-data/integrations/google-ecommerce.md)，您在 [!DNL MBI]? 在本文中，我们将指导您完成构建维度，以将您的电子商务数据与订单和客户数据相关联。

我们涵盖的维度将使您能够构建分析， [回答有关营销渠道和营销活动的重要问题](../../data-analyst/analysis/most-value-source-channel.md). 每个来源的收入占收入的百分比是多少？ 与从以下网站获得的Facebook客户相比，其生命周期价值如何 [!DNL Google]?

## 先决条件和概述

要在本文中创建维度，您需要 [!DNL Google ECommerce] 表格，a `orders` 表和 `customers` 表。 那些桌子一定是 [同步到您的data warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 之后才能构建维度。 同步的表将显示在 `Synced Tables` 部分 `Data Warehouse Manager`.

如果您需要刷新，请快速查看正在同步的表和列：

![](../../assets/Syncing_New_Columns.gif)

从创建连接后 `orders` 表格 [!DNL Google eCommerce] 表格中，我们将创建下面列表中的前三个维度。 接下来，我们使用这些维度在 `customers` 表。 最后，我们将这些列与 `orders` 表。

以下是我们涵盖的维度：

* **订单表**

* Order&#39;s [!DNL Google Analytics] 来源
* Order&#39;s [!DNL Google Analytics] 媒体
* Order&#39;s [!DNL Google Analytics]营销活动
* 客户的首次订购 [!DNL Google Analytics] 来源
* 客户的首次订购 [!DNL Google Analytics] 媒体
* 客户的首次订购 [!DNL Google Analytics] 营销活动

* **客户表**

* 客户的首次订购 [!DNL Google Analytics] 来源
* 客户的首次订购 [!DNL Google Analytics] 媒体
* 客户的首次订购 [!DNL Google Analytics] 营销活动

## 构建维度

要创建维度，请打开 [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 单击 **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 订单表，第1轮

在本例中，我们构建 **Order&#39;s [!DNL Google Analytics] 来源** 维度。

1. 在Data warehouse的表列表中，单击该表(在本例中为 `orders`)。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 选择 `Joined Column` 从 [定义下拉列表](../data-warehouse-mgr/calc-column-types.md). 在本例中，我们使用 [一对一关系](../data-warehouse-mgr/table-relationships.md)，与 `eCommerce.transactionID` 列到 `orders` 表。
1. 接下来，我们需要定义路径，或正在使用的表和列如何连接。 单击 `Select a table and column` 下拉列表。
1. 我们需要的路径不可用，因此我们需要创建一个新路径。 单击 **[!UICONTROL Create new Path]**.
1. 在显示的窗口中，将 `Many` 侧向 `orders.order\_id`，或 `orders` 包含订单ID的表。
1. 在 `One` 侧，查找 `Google ECommerce` 表，然后将列设置为 `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 单击 **[!UICONTROL Save]** 创建路径。
1. 添加路径后，单击 **[!UICONTROL Select table and column]** 再次下拉。
1. 找到 `ECommerce` 表格，然后单击 `Source` 列。 这会将订单与源信息绑定。
1. 返回表模式后，单击 **[!UICONTROL Save]** 再次创建维度。

以下是整个过程：

![](../../assets/help_center.gif)

接下来，尝试创建 **Order&#39;s [!DNL Google Analytics] 媒体** 和 `campaign`. 这些维度不会有太大变化，请尝试一下。 但如果你卡住了，你可以查 [本文的结尾](#stuck) 看看有什么不同。

### 客户表 {#customers}

在本例中，我们构建 **客户的首次订购 [!DNL Google Analytics] 来源** 维度。

1. 在Data warehouse的表列表中，单击该表(在本例中为 `customers`)，其中包含您的客户信息。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 在本例中，我们选择 `is MAX` 定义 [定义下拉列表](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 的 `is MIN` 如果应用到只具有一个可能值的文本列，则也可以使用定义。 重要的部分是确保设置正确的过滤器，我们稍后会这样做。
1. 单击 **[!UICONTROL Select a table and column]** 下拉菜单，然后选择 `orders` 表格，然后 `Order's [!DNL Google Analytics] source` 列。
1. 单击 **[!UICONTROL Save]**.
1. 返回表模式后，单击 `Options` 下拉列表，然后 `Filters`.
1. 单击 **[!UICONTROL Add Filter Set]** ，然后选择 `Orders we count` 设置。 我们只希望将包含在计数过滤器集中的订单中的订单包含在内，因此选择此过滤器集很重要。
1. 单击 **[!UICONTROL Add Filter]**. 我们想找到顾客的首笔订单 [!DNL Google Analytics] 来源，因此我们需要添加过滤器：

   _orders.客户的订单编号= 1

   _
1. 单击 **[!UICONTROL Save]** 创建维度。

接下来，尝试创建 **客户的首次订购 [!DNL Google Analytics] 媒体** 和 `campaign`. 这些维度不会有太大变化，请尝试一下。 但如果你卡住了，你可以查 [本文的结尾](#stuck) 看看有什么不同。

### 附加：订单表，第2轮

如果需要，您可以停止在此处，但此部分将 **客户的首次订购 [!DNL Google Analytics] 维度** 我们在 [最后部分](#customers) 到 `orders` 表。 通过在此部分中创建维度，可分析基于 `orders` 表 —  `Revenue`, `Number of orders`, `Distinct buyers`、等 — 使用 [!DNL Google Analytics] 客户首次订单的属性。

在本例中，我们加入 `Customer's first order's [!DNL Google Analytics] source` 维度 `orders` 表。

1. 在Data warehouse的表列表中，单击该表(在本例中为 `orders`)。
1. 单击 **[!UICONTROL Create a Column]**.
1. 命名列。
1. 选择 `Joined Column` 从定义下拉列表中。 这会将您在上一部分中创建的客户维度与 `orders` 表。
1. 单击 **[!UICONTROL Select a table and column]** 下拉菜单，然后选择 `customers` 表格和 `Customer's first order's [!DNL Google Analytics] source` 列。
1. 如果路径没有自动填充，请选择最能连接客户和订单表的路径。
1. 单击 **[!UICONTROL Save]** 创建维度。

以下是整个过程：

![](../../assets/help_center2.gif)

最后，加入 `Customer's first order's` 媒介和 `campaign` 维度 `orders` 表。 试试看，正如我们之前提到的，请看 [文章的结尾](#stuck) 如果你需要帮助。

### 包装

我们完成了维度的创建，这意味着我们现在可以创建功能强大的分析来跟踪各种渠道和营销活动的效果。 我们知道你急切地想开始，但请记住 **新列只有在下次更新完成后才可用**.

我们在本文中介绍了一些比较流行的维度，但天空是极限 — 尝试创建您自己的维度，或者如果您希望帮助探索其他选项，可以随意地ping我们。 

### 我卡住了！ 有什么不同？ {#stuck}

**`Orders`表#1:** 创建 `Order's [!DNL Google Analytics]` 媒介和 `campaign` 维度中，差异将是在步骤12中选择的列。 在本例中，该列为 `Source`.

**`Customers`表：** 创建 `Customer's first order's [!DNL Google Analytics]` 媒介和 `campaign` 维度中，不同之处在于步骤5中选择的列。 在本例中，该列为 `Order's [!DNL Google Analytics]` 来源。

**`Orders`表#2:** 加入 `Customer's first order's [!DNL Google Analytics]` 媒介和 `campaign` 列 `orders` 表格中，不同之处在于步骤5中选择的列。 在本例中，该列为 `Customer's first order's [!DNL Google Analytics]` 来源。
