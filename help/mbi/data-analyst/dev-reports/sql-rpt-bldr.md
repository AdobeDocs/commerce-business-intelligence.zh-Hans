---
title: 使用SQLReport Builder
description: 了解使用SQLReport Builder的细节。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 0%

---

# 使用[!DNL SQL Report Builder]

>[!NOTE]
>
>需要[管理员权限](../../administrator/user-management/user-management.md)才能创建和编辑SQL图表。 `Standard`用户可以在功能板上重新排列这些图表，并且`Read-only`用户具有与传统图表相同的体验。 此外，`Read-only`用户无权访问查询的文本。

请观看[培训视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html)以了解更多信息。

[!DNL SQL]或结构化查询语言是一种用于与数据库通信的编程语言。 在[!DNL Commerce Intelligence]中，[!DNL SQL]用于查询或检索您Data Warehouse中的数据。 查看仪表板上的报告 — 幕后，每个报告都由[!DNL SQL]查询提供支持。

您可以使用[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)直接查询您的Data Warehouse、查看结果并将其转换为图表。 您可以通过单击&#x200B;**[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**&#x200B;开始使用[!DNL SQL Report Builder]创建报告。

请观看[培训视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html)以了解更多信息。

[!DNL SQL Report Builder]允许您直接查询Data Warehouse、查看结果并快速将其转换为图表。 使用[!DNL SQL]生成报告的最好部分是您不需要等待更新周期来迭代您创建的列。 如果结果不正确，您可以快速编辑并重新运行查询，直到符合您的预期为止。

本主题将指导您使用[!DNL SQL Report Builder]。 在您熟悉情况后，请查看可视化图表的[!DNL SQL]教程或尝试优化您编写的某些查询。

本文涵盖的内容：

1. [编写查询](#writing)

1. [运行查询并查看结果](#runquery)

1. [创建可视化图表](#createviz)

1. [保存报告](#save)

## [!DNL SQL Report Builder]集成

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md)是唯一不可与[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)一起使用的集成。 此功能正在开发中。

要开始创建[!DNL SQL]报告，请单击任意仪表板顶部的&#x200B;**[!UICONTROL Report Builder]**&#x200B;或&#x200B;**[!UICONTROL Add Report]**。 在[!DNL Report Picker]屏幕中，单击&#x200B;**[!UICONTROL SQL Report Builder]**&#x200B;以打开[!DNL SQL]编辑器。

## 开始使用

要编辑报告，请单击基于[!DNL SQL]的图表右上角的齿轮(![](../../assets/gear-icon.png))图标，然后单击&#x200B;**[!UICONTROL Edit]**。

## 编写查询 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder]查询区分大小写。 请确保您在编写查询时使用正确的大小写，否则您可能会收到意外的结果或错误。

按照查询优化](../../best-practices/optimizing-your-sql-queries.md)的[准则，在[!DNL SQL]编辑器中编写查询。

>[!IMPORTANT]
>
>**[!DNL SQL]报表中的量度** — 将量度插入到SQL报表中时，将使用量度的`current definition`。

如果度量将来更新，则SQL报表&#x200B;*不会*&#x200B;反映这些更改。 您必须手动编辑报告以使更改生效。

使用侧边栏顶部的按钮，您可以在表列表与[!DNL SQL Report Builder]中可用的量度之间切换。 如果您在列表中看不到要查找的内容，请尝试使用侧栏顶部的搜索栏进行搜索。

您还可以使用[!DNL SQL]编辑器中的侧边栏，通过将鼠标悬停在量度、表和列上并单击&#x200B;**[!UICONTROL Insert]**，将其直接插入到查询中：

![正在将表插入到[!DNL SQL]编辑器中。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>SQLReport Builder支持PostgreSQL支持的任何[SELECT函数](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)或任何不改变数据的函数。 这包括但不限于AVG、COUNT、COUNT DISTINCT、MIN/MAX和SUM。

此外，支持任何`JOIN`类型，但Adobe建议仅使用INNER JOIN，因为它是最便宜的`JOIN`类型。

## 运行查询并查看结果 {#runquery}

完成查询编写后，单击&#x200B;**[!UICONTROL Run Query]**。 结果显示在SQL编辑器下方的表中：

![正在运行查询并查看结果。](../../assets/SQL_Run_Query.gif)

如果结果中有出错的地方，您可以编辑查询并重新运行它，直到满意为止。

有时您可能会看到编辑器中包含EXPLAIN的[消息](../../best-practices/optimizing-your-sql-queries.md)。 如果您看到其中一个，则表示您的查询尚未运行，需要微调一下。

编辑完查询后，您可以转到创建可视化图表或将您的工作保存到功能板。

## 创建可视化图表 {#createviz}

若要使用查询结果创建可视化图表，请单击`Results`窗格中的&#x200B;**[!UICONTROL Chart]**&#x200B;选项卡。 在此选项卡中，选择：

* `Series`或您要测量的列，如&#x200B;**售出的商品**。
* `Category`或要用于划分数据的列，如&#x200B;**客户获取源**。
* `Labels`或X轴值。

下面是可视化流程的外观：

![](../../assets/SQL_RB_viz_overview.gif)

有关如何创建可视化图表的详细演练，请参阅[从SQL查询创建可视化图表教程](../../tutorials/create-visuals-from-sql.md){： target=&quot;_blank&quot;}。

## 保存报告 {#save}

在保存所做的工作之前，必须为报表提供一个名称。 请记住遵循[命名](../../best-practices/naming-elements.md)的最佳实践指南{： target=&quot;_blank&quot;}，并选择能清晰传达报告内容的内容！

单击[!DNL SQL]编辑器右上角的&#x200B;**[!UICONTROL Save]**&#x200B;并选择报告`Type` （`Chart`或`Table`）。 要完成任务，请选择报告要保存到的仪表板，然后单击&#x200B;**[!UICONTROL Save to Dashboard]**。

![](../../assets/SQL_Save_Report.gif)

### 分析您的数据

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)让您能够直接查询Data Warehouse、查看结果，并快速将其转换为报表。 使用[!DNL SQL]还允许您[使用`Visual`或`Cohort`Report Builder中不可用的 [!DNL SQL] 函数](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，从而让您更好地控制数据。

使用[!DNL SQL]创建的计算列不依赖于更新周期，这意味着您可以按自己的意愿对其进行迭代，并立即查看结果。

>[!NOTE]
>
>这仅适用于列的结构，而不适用于数据的新鲜度。 新数据仍依赖于已成功完成的更新周期。

| **这非常适合于……** | **这不太适合……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要了解[!DNL SQL]。 |
| [!DNL SQL]精通 | 简单分析 — 编写查询可能比简单地使用[!UICONTROL Visual Report Builder]更有效。 |
| 构建一次性使用的计算列 | 与他人共享 — 考虑您的受众：他们了解[!DNL SQL]吗？ 否则，他们可能会对构建报表的方式感到困惑。 |
| 具有`one-to-many`关系的数据 |  |
| 测试新列或分析 |  |

#### 数据库与SQL编辑器结果

大多数情况下，结果的差异可归因于更新周期。 如果[!DNL Commerce Intelligence]正在将数据从数据库复制到Data Warehouse，则即使使用相同的查询，您也可能会看到不同的结果。

连接问题也会导致不一致。 通过单击&#x200B;**[!DNL Manage Data** > **Connections]**&#x200B;导航到`Connections`页面以将其签出 — 相关数据库集成是否存在错误？ 如果出现这种情况，您可能需要[重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)才能使集成重新运行。

如果所有集成都连接成功，并且您未处于更新周期中，则可能有其他错误。

#### 删除[!DNL SQL]报告是否也会从我的Data Warehouse中删除基础列？

不需要，无论如何构建Data Warehouse，您都不会丢失任何列。

如果删除使用`Data Warehouse Manager`的报表或查询，则使用创建的列不会受到影响。

使用[!DNL SQL Report Builder]创建的列未保存到Data Warehouse。


#### `Report Builder`与`SQL Report Builder`

[!DNL SQL Report Builder]让您在创建和构建图表时拥有更大的灵活性 — 例如，您可以选择在`X`轴和`Y`轴上应显示的值。 有关在[!DNL SQL Report Builder]中创建图表的详细信息，请参阅[从 [!DNL SQL] 查询创建可视化图表](../../tutorials/create-visuals-from-sql.md)教程。

#### `Cohort Report Builder` {#cohortrb}

与[!DNL Visual Report Builder]不同，[[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md)仅用于一个目的 — 分析和识别一段时间内相似用户组的行为趋势。 使用[!DNL Cohort Report Builder]不需要任何[!DNL SQL]知识，因此，如果您刚刚开始，可以毫不犹豫地直接开始使用。

| **这非常适合于……** | **这不太适合……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要定义练习的同类群组。 |
| 确定一段时间内的行为趋势 | 定性分析 — 它可以[完成](../dev-reports/create-qual-cohort-analysis.md)，但需要Adobe帮助。 |

## 在更新周期后重建查询

您不必重新生成查询。 使用[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)创建的报告将像在传统`Report Builder`中创建的报告一样保存。 [!DNL SQL]图表的更新过程相同 — 更新数据后，图表中的值将重新计算并重新显示。

>[!NOTE]
>
>删除[!DNL SQL]报表/查询时，不会从Data Warehouse中删除基础列。 无论如何构建列，都不会丢失任何列。

* 如果删除使用使用Data Warehouse管理器创建的报表或查询，则这些列不会受到影响。

* 使用SQLReport Builder创建的列不会保存到Data Warehouse中。

## 正在结束 {#wrapup}

如果您希望尝试一些更具挑战性的东西，为什么不尝试编写针对可视化进行了优化的查询？ 要开始操作，请查看[从 [!DNL SQL] 查询创建可视化图表](../../tutorials/create-visuals-from-sql.md){： target=&quot;_blank&quot;}教程。
