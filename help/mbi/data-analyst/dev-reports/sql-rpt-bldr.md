---
title: 使用SQLReport Builder
description: 了解使用SQLReport Builder的进出。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 0%

---

# 使用 `SQL Report Builder`

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md) 创建和编辑SQL图表。 `Standard` 用户可以在功能板上重新排列这些图表， `Read-only` 用户将拥有与传统图表相同的体验。 此外， `Read-only` 用户无权访问查询的文本。

查看我们的 [培训视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) 以了解更多。

`SQL`，或结构化查询语言，是一种用于与数据库通信的编程语言。 在 [!DNL MBI], SQL用于查询或检索data warehouse中的数据。 查看功能板上的报表 — 在后台，每个报表都由SQL查询提供支持。

您可以使用 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 要直接查询data warehouse，请查看结果，并将它们转换为图表。 您可以开始使用 `SQL Report Builder` 导航至 **[!UICONTROL Report Builder** > **SQL Report Builder]**.

查看我们的 [培训视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) 以了解更多。

的 `SQL Report Builder` 允许您直接查询data warehouse、查看结果，并快速将它们转换为图表。 使用SQL构建报告的最好部分是，您无需等待更新周期，即可在您创建的列上进行迭代。 如果结果不太正确，您可以快速编辑并重新运行查询，直到这些内容符合您的预期。

在本文中，我们将指导您使用 `SQL Report Builder`. 了解您的方法后，请查看我们的SQL以了解可视化教程，或尝试优化您编写的一些查询。

以下是本文所涵盖内容的概述：

1. [编写查询](#writing)

1. [运行查询并查看结果](#runquery)

1. [创建可视化图表](#createviz)

1. [保存报表](#save)

## SQLReport Builder集成

在当今世界， [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) 是唯一无法与 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). 我们正在努力在以后的版本中包含此功能。

要开始创建新的SQL报告，请单击 **[!UICONTROL Report Builder]** 或 **[!UICONTROL Add Report]** 的双曲正切值。 在 `Report Picker` 屏幕，单击 **[!UICONTROL SQL Report Builder]** 打开SQL编辑器。

## 入门

要编辑报表，请单击齿轮(![](../../assets/gear-icon.png))图标，然后单击 **[!UICONTROL Edit]**.

## 编写查询 {#writing}

>[!NOTE]
>
>`SQL Report Builder` 查询区分大小写。 确保在编写查询时使用正确的大小写，否则可能会出现意外结果或错误。

关注 [查询优化准则](../../best-practices/optimizing-your-sql-queries.md)，在SQL编辑器中写入查询。

>[!IMPORTANT]
>
>**SQL报表中的量度**  — 在SQL报表中插入量度时， `current definition` 的值。

如果量度将来更新，则SQL报告 *将不会* 反映更改。 您必须手动编辑报表才能使更改生效。

使用侧栏顶部的按钮，您可以在可用于 `SQL Report Builder`. 如果您在列表中未看到要查找的内容，请尝试使用侧栏顶部的搜索栏进行搜索。

您还可以使用SQL编辑器中的侧栏将量度、表和列直接插入查询中，方法是将鼠标悬停在查询上并单击 **[!UICONTROL Insert]**:

![在SQL编辑器中插入表。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>任意 [SELECT函数](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)，或任何不改变数据的函数（PostgreSQL支持）均在SQLReport Builder中受支持。 这包括但不限于AVG、COUNT、COUNT DISTINCT、MIN/MAX和SUM。

此外，支持任何JOIN类型，但我们建议仅使用INNER JOIN，因为它是JOIN类型中最便宜的。

## 运行查询并查看结果 {#runquery}

完成编写查询后，单击 **[!UICONTROL Run Query]**. 结果将显示在SQL编辑器下的表中：

![运行查询并查看结果。](../../assets/SQL_Run_Query.gif)

如果结果中出现某些内容，您可以编辑查询并重新运行该查询，直到您满意为止。

您有时可能会看到 [编辑器下带有EXPLAIN的消息](../../best-practices/optimizing-your-sql-queries.md). 如果您看到其中一个，则表示您的查询尚未运行，需要进行一些微调。

编辑完查询后，您可以转到创建可视化或将工作保存到功能板。

## 创建可视化图表 {#createviz}

要使用查询结果创建可视化，请单击 **[!UICONTROL Chart]** 选项卡 `Results` 中。 在此选项卡中，您将选择：

* 的 `Series`，或要测量的列，例如 **已售项目**.
* 的 `Category`，或要用于划分数据的列，例如 **客户获取源**.
* 的 `Labels`，或X轴值。

以下是可视化图表过程的外观：

![](../../assets/SQL_RB_viz_overview.gif)

有关如何创建可视化的详细说明，请参阅 [从SQL查询创建可视化教程](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;}。

## 保存报表 {#save}

在保存您的工作之前，必须为报表提供一个名称。 请记住，请遵循 [命名的最佳实践准则](../../best-practices/naming-elements.md){:target=&quot;_blank&quot;}并选择明确传达报表内容的内容！

单击 **[!UICONTROL Save]** 在SQL编辑器的右上角，选择报表 `Type` (`Chart` 或 `Table`)。 要进行总结，请选择要保存报表的功能板，然后单击 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### 分析数据

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 允许您直接查询data warehouse、查看结果并快速将结果转换为报表。 使用SQL还允许您 [使用不可用的SQL函数](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 在 `Visual` 或 `Cohort` Report Builder，从而让您能够更好地控制数据。

我们要提及的是，使用SQL创建的计算列不依赖于更新周期，这意味着您可以按要求对它们进行迭代，并立即看到结果。

>[!NOTE]
>
>这仅适用于列的结构，而不适用于数据的刷新。 新数据仍取决于成功完成的更新周期。

| **这是完美的……** | **这对……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要了解SQL。 |
| 精通SQL | 简单分析 — 编写查询比简单地使用可视化Report Builder更有效。 |
| 构建一次性使用的计算列 | 与他人共享 — 请考虑您的受众：他们懂SQL吗？ 如果没有，他们可能会对如何构建报表感到困惑。 |
| 数据 `one-to-many` 关系 |  |
| 测试新列或分析 |  |

#### 数据库与SQL编辑器结果

大多数时间、结果差异都可归因于更新周期。 如果 [!DNL MBI] 正在将数据从数据库复制到Data warehouse的过程中，即使使用同一查询，您也可能会看到不同的结果。

连接问题也可能导致差异。 导航到 `Connections` 通过单击 **[!DNL Manage Data** > **Connections]**)进行检查 — 有关数据库集成是否有错误？ 如果是，您可能需要 [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) 让事情重新运行。

如果所有集成均已成功连接，并且您未在更新周期的中间，则可能会出现其他问题。

#### 删除SQL报表是否也会从我的Data warehouse中删除基础列？

不会，无论您是如何构建列的，您都不会从Data warehouse中丢失任何列。

使用创建的列 `Data Warehouse Manager` 如果删除使用报表或查询，则不会受到影响。

使用创建的列 `SQL Report Builder` 未保存到您的Data warehouse。


#### `Report Builder` 与 `SQL Report Builder`

的 `SQL Report Builder` 在创建和构建图表时，可以更加灵活 — 例如，您可以选择应显示在上的值 `X` 和 `Y` 轴。 有关在 `SQL Report Builder`，请查看我们的 [从SQL查询创建可视化](../../tutorials/create-visuals-from-sql.md) 教程。

#### `Cohort Report Builder` {#cohortrb}

与 `Visual Report Builder`, [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 仅用于一个目的 — 分析和识别一段时间内类似用户组的行为趋势。 使用同类群组Report Builder不需要具备任何SQL知识，因此，如果您刚开始使用，可以毫不犹豫地直接入门。

| **这是完美的……** | **这对……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要练习定义同类群组。 |
| 确定一段时间内的行为趋势 | 定性分析 — 可以 [完成](../dev-reports/create-qual-cohort-analysis.md)，但需要我们的帮助。 |

## 更新周期后重建查询

您不必重新构建查询。 使用创建的报表 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) 与传统 `Report Builder`. SQL图表的更新过程完全相同 — 更新数据后，将重新计算并重新显示图表中的值。

>[!NOTE]
>
>删除SQL报表/查询时，不会从Data warehouse中删除基础列。 无论您是如何构建列的，列都不会丢失。

* 如果删除使用Data warehouse管理器的报表或查询，则使用该管理器创建的列将不会受到影响。

* 使用SQLReport Builder创建的列不会保存到您的Data warehouse。

## 包装 {#wrapup}

如果您想尝试更具挑战性的内容，何不尝试编写针对可视化图表优化的查询？ 看看我们的 [从SQL查询创建可视化教程](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;}以开始操作。
