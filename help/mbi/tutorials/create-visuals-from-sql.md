---
title: 通过SQL查询创建可视化图表
description: 了解如何熟悉SQL Report Builder中使用的术语，并为您创建SQL可视化图表奠定坚实的基础。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 通过SQL查询创建可视化图表

本教程的目标是熟悉[!DNL SQL Report Builder]中使用的术语，并为您创建`SQL visualizations`奠定坚实的基础。

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md)是一个带有选项的Report Builder：您可以仅出于检索数据表的目的运行查询，也可以将这些结果转换为报表。 本教程介绍如何从SQL查询构建可视化图表。

## 术语

在开始本教程之前，请参阅`SQL Report Builder`中使用的以下术语。

- `Series`：您要测量的列在SQL Report Builder中称为序列。 常见示例为`revenue`、`items sold`和`marketing spend`。 必须至少将一列设置为`Series`才能创建可视化图表。

- `Category`：要用于划分数据的列称为`Category`，这与`Group By`中的[`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md)功能类似。 例如，如果要按客户的客户获取来源对客户的存留期收入进行分段，则将包含客户获取来源的列指定为`Category`。 可以将多个列设置为`Category`。

>[!NOTE]
>
>日期和时间戳也可用作`Categories`。 它们只是查询中的另一列数据，必须在查询本身中根据需要进行格式化和排序。

- `Labels`：这些标签应用为x轴标签。 在分析随时间变化的数据趋势时，将年和月列指定为标签。 可以将多个列设置为“标签”。

## 步骤1：编写查询

请牢记以下内容：

- [!DNL SQL Report Builder]使用[`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html)。

- 如果要创建具有时间系列的报告，请务必`ORDER BY`时间戳列。 这可确保时间戳在报表中以正确的顺序绘制。

- `EXTRACT`函数非常适合用于解析时间戳的日、周、月或年。 当您要在报表上使用的`time interval`为`daily`、`weekly`、`monthly`或`yearly`时，这将很有用。

若要开始，请单击[!DNL SQL Report Builder]打开&#x200B;**[!UICONTROL Report Builder** > **SQL Report Builder]**。

例如，考虑此查询，该查询返回每个产品每月的销售项目总数：

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

此查询返回此结果表：

![](../assets/SQL_results_table.png)

## 第2步：创建可视化图表

使用这些结果，*您如何创建可视化图表？*&#x200B;若要开始，请单击&#x200B;**[!UICONTROL Chart]**&#x200B;窗格中的`Results`选项卡。 这会显示`Chart settings`选项卡。

首次执行查询时，报告可能看起来不可靠，因为查询中的所有列都绘制为系列：

![](../assets/SQL_initial_report_results.png)

对于此示例，您希望这是一段时间内趋势的折线图。 要创建它，请使用以下设置：

- `Series`：选择`Items sold`列作为`Series`，因为您希望对其进行度量。 定义`Series`列后，您将在报表中看到绘制的一行。

- `Category`：对于此示例，您希望将每个产品作为报告中的不同行查看。 为此，您将`Product name`设置为`Category`。

- `Labels`：使用列`year`和`month`作为x轴上的标签，以便能够查看`Items Sold`随时间变化的趋势。

>[!NOTE]
>
>如果标签是`ORDER BY`/`date`列，查询必须包含标签上的`time`子句。

下面是您如何创建此可视化图表的概览，从运行查询到设置报表：

![](../assets/SQL_report_settings.gif)

## 步骤3：选择`Chart Type`

此示例使用`Line`图表类型。 要使用其他`chart type`，请单击图表选项部分上方的图标进行更改：

![](../assets/Chart_types.png)

## 步骤4：保存可视化图表

如果要再次使用此报表，请为该报表命名，然后单击右上角的&#x200B;**[!UICONTROL Save]**。

在下拉菜单中，选择`Chart`作为`Type`，然后选择要将报告保存到的仪表板。

## 正在结束

想更进一步吗？ 查看[查询优化最佳实践](../best-practices/optimizing-your-sql-queries.md)。
