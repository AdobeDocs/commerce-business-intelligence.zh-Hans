---
title: data warehouse管理器
description: 了解如何管理表和列同步设置，深入到表的架构中，以及创建要在报表中使用的计算列。
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# data warehouse管理器

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md)

data warehouse管理器，通过单击 **[!UICONTROL Manage Data > Data Warehouse]** 在侧栏中，是您的 [!DNL MBI] data warehouse。 使用Data warehouse管理器，您可以管理表和列同步设置，深入到表的架构中，并创建要在报表中使用的计算列。

在本文中，我们将介绍：

* [学习周游](#learning)
* [正在同步表和列](#syncing)
* [创建计算列](#calculated)
* [删除表和删除列](#delete)
* [在后台同步新表](#syncnew)
* [那么，我什么时候才能使用新列？](#when)

## 学习周游 {#learning}

的左侧 `Data Warehouse Manager` 页面包含表列表，允许您轻松地在表之间切换。 从列表中选择表时，表管理区域将使用表的架构填充，在该架构中可以更改所选表。

在表列表中，表按其连接源进行分组。 这些源将添加在 [!UICONTROL Manage Data > Integrations] 可能是数据库， [API](https://developer.adobe.com/commerce/services/reporting/)或第三方连接器。 表格列表顶部有一个搜索框，使您能够轻松查找所需的表格。

在搜索框下，您将看到两个选项： `All Tables` 和 `Synced Tables`. 的 `All Tables` 选项列出了您为Data warehouse提供的所有表，其中包括已同步和未同步的表。

的 `Synced Tables` 选项显示已添加到Data warehouse并且已从选定列复制数据的所有表。

在 `All Tables` 列表？ 原因可能有以下几点：

* 尚未添加数据源
* 数据源是数据库， [!DNL MBI] 您创建的用户无权访问。 在这种情况下，您或您的数据库管理员需要授予访问权限。
* 数据源或表最近添加，尚未同步

## 正在同步表和列 {#syncing}

### 正在同步新表和本机列

data warehouse管理器不仅让您能够轻松查看和管理数据源，还允许您选择要同步的各个表和列。

1. 单击 `All Tables` 选项，然后找到要同步的表。
1. 单击表的名称以预览架构。 如果表为新表，则所有列将显示为 `Unsynced`.
1. 检查要同步的列。

   >[!NOTE]
   >
   >表的本机列将在 `Location` 列。

1. 请务必检查 `Primary Key` 列 — 这些列的列名称旁有一个键符号。 A `Primary Key` 需要才能将数据正确同步到Data warehouse。

   如果正在同步直接从数据库访问的表，则可能 `Primary Keys` 不能表示。 在这种情况下，请与数据库管理员联系以请求将主密钥或密钥添加到表中。
1. 完成后，单击 ![按钮](../../assets/button.png) 按钮。

A *成功！* 将显示消息，状态将更改为 `Pending` 列。 下次完全更新后，新同步的表和列将可在报表中使用；您还可以设置新 [复制方法](./cfg-replication-methods.md) 初始同步之后。

以下是整个过程的概览：

![向data warehouse添加列](../../assets/DW_sync.gif)

### 在后台同步新表 {#syncnew}

首次同步大型新表时，您的data warehouse需要以追溯方式捕获表中的所有数据点，然后才能持续捕获新数据。 如果表格特别大，则可能不希望该初始同步与 **更新周期**  — 在这种情况下，您希望初始同步在后台进行，在 *并行* 当前运行的任何更新。

要确保发生这种情况，您应选择 `Save and Sync Data Immediately` 选项首次同步该表。

### 检查新表和列 {#forceupdate}

您的Data warehouse在添加新源、表或列时不会自动检测它们。 同步过程会在一周内运行，以查找新的添加项并使其可用，但是如果要在该过程运行之前访问新添加的表和列，则可以强制执行结构同步。

表格列表中搜索栏的下方是 `Check for new tables and columns` 链接。 单击此链接将强制启动结构同步过程；通常在10分钟后提供新增内容。 刷新页面以查看新的源、表或列。

## 创建计算列 {#calculated}

仅仅能够查看和管理所有来源的数据，就可以更轻松地洞察您的业务。 但是，在Data warehouse管理器中，您能够通过在表内创建计算列来更进一步。 `Calculated` 列从现有数据派生新信息。

假设您要添加 `user's lifetime revenue` 至 `users` 表格，查找高价值用户。 或者，如果要按性别划分收入，可以添加 `customer's gender` 至 `orders` 表。

为帮助您主控创建这些列， [我们创建了一个教程](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md) 来带你过去。

## 删除表和删除列 {#delete}

正如您能够选择要同步到Data warehouse的表和列一样，您也能够拖放或删除表和列。

>[!NOTE]
>
>在确认删除后，删除表或删除列将删除任何从属报表、量度、过滤集和列。 你一定要这么做。 **此操作无法撤消。**

单击 **[!UICONTROL Delete]** 意外。 依赖关系检查会在任何内容被删除之前运行，因此您有机会在确认之前查看所有内容。

要删除列，请单击列所属的表。 选中要删除的列，然后单击 ![button\_1.png](../../assets/button_1.png) 按钮。

要删除已同步的表，请选择表中的所有列，然后再次单击 ![按钮](../../assets/button_1.png) 按钮。 这将从您的data warehouse中删除使用此表的所有本机列和计算列。

### 确认更改

无论是删除表还是删除列，都会在删除过程完成之前运行依赖关系检查。 依赖关系是利用要删除的表或列的计算列、量度、过滤器集和报表。 将显示任何已发现的依赖项 — 此时，您可以取消该过程或单击 **[!UICONTROL Confirm Changes]** 删除表/删除列。

虽然删除的依赖关系无法还原，但如果将来需要重新同步任何本机列，表和列仍将可用。

以下是删除列的快速说明：

![从data warehouse中删除列](../../assets/DW_delete.gif)

## 那么，我什么时候才能使用新列？ {#when}

新同步的列和新的/更新的计算列将在下次完全更新完成后准备就绪以供使用。 如果更新尚未进行，可通过单击 **[!UICONTROL Force update]** 显示在 `Data Warehouse` 或 `Integrations` 页面。 您还可以通过单击 **[!UICONTROL Email me when complete]**.

当您准备好在报表中使用新列时， [您需要先将它们添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md). 尽管数据在更新完成后才可用，但您仍可以在报表中使用新列。 更新完成后，将显示报表中的数据。

## 就是这样，我们到了最后！

我们在本教程中介绍了许多材料。 现在，您应该对数据库是什么、数据的组织方式、表如何彼此关联以及使用Data warehouse管理器可以执行的操作有了透彻的了解。

太棒了！ 通过 [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) 或 [做一些有趣的报告](../../tutorials/using-visual-report-builder.md).
