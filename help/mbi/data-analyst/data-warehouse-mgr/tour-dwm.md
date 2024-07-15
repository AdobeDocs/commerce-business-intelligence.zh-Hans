---
title: Data Warehouse管理器
description: 了解如何管理表和列同步设置、深入了解表的架构以及创建计算列以在报告中使用。
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Data Warehouse管理器

>[!NOTE]
>
>需要[管理员权限](../../administrator/user-management/user-management.md)

通过单击&#x200B;**[!UICONTROL Manage Data > Data Warehouse]**&#x200B;访问的Data Warehouse管理器是您[!DNL Adobe Commerce Intelligence]Data Warehouse的门户。 使用Data Warehouse管理器，您可以管理表和列同步设置、深入查看表的架构以及创建计算列以在报告中使用。

本主题涵盖：

* [了解如何应对挑战](#learning)
* [正在同步表和列](#syncing)
* [创建计算列](#calculated)
* [删除表和删除列](#delete)
* [在后台同步新表](#syncnew)
* [那么，我什么时候可以使用我的新栏呢？](#when)

## 了解如何应对挑战 {#learning}

`Data Warehouse Manager`页的左侧包含表列表，可让您轻松地在表之间进行切换。 从列表中选择表时，表管理区域将填充表的方案，您可以在其中修改所选表。

在表列表中，表按其连接源分组。 这些源添加到[!UICONTROL Manage Data > Integrations]下，可以是数据库、[API](https://developer.adobe.com/commerce/services/reporting/)或第三方连接器。 在表列表顶部有一个搜索框，通过该框可以轻松查找所需的表。

在搜索框下，您看到两个选项：`All Tables`和`Synced Tables`。 `All Tables`选项列出您对Data Warehouse可用的所有表，包括已同步和未同步的表。

`Synced Tables`选项显示已添加到Data Warehouse中且从选定列复制数据的所有表。

在`All Tables`列表中看不到您要查找的表？ 这种情况有几个可能的原因：

* 尚未添加数据源
* 数据源是一个数据库，而您创建的[!DNL Commerce Intelligence]用户没有访问权限。 在这种情况下，您或您的数据库管理员必须授予访问权限。
* 数据源或表最近已添加且尚未同步

## 正在同步表和列 {#syncing}

### 正在同步新表和本机列

Data Warehouse管理器不仅让您能够轻松查看和管理数据源，而且您还可以自由选择要同步的单个表和列。

1. 单击`All Tables`选项并找到要同步的表。
1. 单击表的名称以预览架构。 如果是新表，则所有列都显示为`Unsynced`。
1. 选中要同步的列。

   >[!NOTE]
   >
   >表本地的列在`Location`列中具有来自您的数据库的列。

1. 确保检查`Primary Key`列 — 这些列的名称旁边有一个键符号。 需要`Primary Key`才能将数据正确同步到Data Warehouse中。

   如果您正在同步直接来自数据库的表，则可能无法表示`Primary Keys`。 在这种情况下，请与数据库管理员联系以请求向表中添加一个或多个主键。
1. 完成后，单击![按钮](../../assets/button.png)按钮。

*成功！显示*&#x200B;消息，选定列的状态更改为`Pending`。 下次完全更新完成后，新同步的表和列将可用于报告中。 您还可以在初始同步后设置新的[复制方法](./cfg-replication-methods.md)。

下面快速了解一下整个过程：

![正在向数据仓库添加列](../../assets/DW_sync.gif)

### 在后台同步新表 {#syncnew}

首次同步大型表时，Data Warehouse需要先以追溯方式捕获表中的所有数据点，然后再持续捕获新数据。 如果您的表很大，您可能不希望该初始同步与&#x200B;**更新周期**&#x200B;顺序运行。 在这种情况下，您希望初始同步在后台进行，与任何当前运行的更新进行&#x200B;*并行*。

为确保发生这种情况，应选择首次同步该表的`Save and Sync Data Immediately`选项。

### 检查新表和列 {#forceupdate}

在新源、表或列添加后，您的Data Warehouse不会自动检测到它们。 同步进程在一周中运行以查找新的添加项并使它们可用，但如果您要在进程运行之前访问新添加的表和列，则可以强制进行结构同步。

表列表中的搜索栏下方是一个`Check for new tables and columns`链接。 单击此链接将强制启动结构同步过程；新添加内容通常在10分钟后可用。 刷新页面以查看新的源、表或列。

## 创建计算列 {#calculated}

只需能够查看和管理来自所有来源的数据，即可更轻松地获得对业务的洞察。 但在Data Warehouse管理器中，您可以通过在表中创建计算列来更进一步。 `Calculated`列从现有数据派生新信息。

假设您想将`user's lifetime revenue`添加到您的`users`表以查找高价值用户。 或者，如果您要按性别划分收入，可以将`customer's gender`添加到您的`orders`表。

有关详细信息，请查看此[教程](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)。

## 删除表和删除列 {#delete}

正如可以选择要同步到Data Warehouse的表和列一样，也可以删除它们。

>[!NOTE]
>
>一旦确认删除，删除表或删除列将删除所有从属报表、量度、过滤器集和列。 确定要执行此操作 — **此操作无法撤消。**

如果您意外单击&#x200B;**[!UICONTROL Delete]**，请不要担心。 依赖项检查会在删除任何内容之前运行，因此您有机会在确认之前查看所有内容。

要删除列，请单击该列所属的表。 选中要删除的列，然后单击![button\_1.png](../../assets/button_1.png)按钮。

要删除已同步的表，请选择表中的所有列，然后再次单击![按钮](../../assets/button_1.png)按钮。 这会从Data Warehouse中删除使用此表的所有本机列和计算列。

### 确认更改

无论您是删除表还是删除列，都将在删除过程完成之前运行相关性检查。 依赖项是使用要删除的表或列的计算列、量度、过滤器集和报表。 任何发现的依赖项都会显示 — 此时，您可以取消进程或单击&#x200B;**[!UICONTROL Confirm Changes]**&#x200B;以删除表/删除列。

虽然已删除的依赖项无法恢复，但如果您将来需要重新同步任何本机列，表和列将仍然可用。

下面是删除列的简单介绍：

![从数据仓库中删除列](../../assets/DW_delete.gif)

## 那么，我什么时候可以使用我的新栏呢？ {#when}

新的同步列和新的/更新的计算列将在下次完全更新完成后准备使用。 如果更新尚未进行，您可以通过单击`Data Warehouse`或`Integrations`页面顶部显示的&#x200B;**[!UICONTROL Force update]**&#x200B;来强制进行更新。 您还可以在更新完成后单击&#x200B;**[!UICONTROL Email me when complete]**&#x200B;以计划电子邮件通知。

当您准备在报表中使用新列时，[您需要先将它们添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。 虽然在更新完成之前数据不可用，但您仍可以在报表中使用新列。 更新完成后，将显示报表中的数据。

## 正在结束

这篇文章介绍了很多材料。 到现在为止，您应该已经对数据库是什么、数据如何组织、表如何相互关联以及您可以使用Data Warehouse管理器执行什么操作有了深入的了解。

请通过[创建计算列](../data-warehouse-mgr/creating-calculated-columns.md)或[制作一些有趣的报告](../../tutorials/using-visual-report-builder.md)来测试您的知识。
