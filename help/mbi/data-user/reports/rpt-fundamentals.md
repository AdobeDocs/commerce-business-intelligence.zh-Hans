---
title: 使用报表
description: 了解如何使用报表数据。
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 使用报表

使用[!DNL Adobe Commerce Intelligence]中的报告帮助您回答业务问题 — 您是只想查看与去年相比的本月收入还是想了解您最新[!DNL Google AdWords]营销活动的客户获取成本。

从提问到回答的路径到底是什么样的？

为了帮助您可视化此流程，该路由如下图所示。 本主题说明了如何解决分析问题，以及获取所需数据所需的后端后勤工作。

## 从问题开始

您知道，为了改善您的业务，您不断地提出各种问题，从提高客户满意度到削减供应成本。 您专注于如何将您的问题转化为可帮助您制定决策的分析。

对于此示例，假设您要回答以下问题：

* 我的新注册者转换速度如何？

## 识别测量

现在是时候确定一份可能的分析和衡量指标清单来帮助回答这个问题了。 对于此示例，请重点关注以下量度：

* 每次使用从注册到首次购买日期的平均时间。

这显示了注册日期和用户首次购买日期之间经过的平均时间，并提供了有关用户在转化漏斗中完成此最后步骤时的行为方式的信息。

## 查找数据

了解应该衡量什么只能让我们在一定程度上实现目标。 要评估每位用户从注册到首次购买日期的平均时间，您需要确定由测量组成的所有数据点。

将度量划分为其核心组件。 您必须了解已注册的人数、购买者的数量以及两次事件之间经过的时间。

在更高级别上，您需要知道在数据库中从何处查找此数据，特别是：

* 该表在每次有人注册时记录一行数据
* 记录每次有人购买时的数据行的表
* 可用于将`purchase`表连接或引用到`customer`表的列 — 这允许我们了解谁购买了

在更精细的粒度级别，您需要确定用于此分析的确切数据字段：

* 包含客户注册日期的数据表和列：例如`user.created\_at`
* 包含购买日期的数据表和列：例如`order.created\_at`

## 创建数据列以供分析

除了上面介绍的本机数据列之外，您还需要一组计算的数据字段来启用此分析，包括：

* `Customer's first purchase date`返回特定用户的`MIN(order.created_at`)

然后用于创建：

* `Time between a customer's registration date and first purchase date`，返回从注册到首次购买之间经过的特定用户时间。 这是您以后量度的基础。

这两个字段都需要在用户级别创建（例如，在`user`表中）。 这使得平均分析可由用户标准化（换句话说，此平均计算中的分母是用户计数）。

这是[!DNL Commerce Intelligence]进入的位置！ 您可以使用[!DNL Commerce Intelligence]Data Warehouse创建上述列。 请联系Adobe分析团队，为我们提供用于创建的新列的特定定义。 您还可以使用[列编辑器](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)。

最佳做法是避免直接在数据库中创建这些计算数据字段，因为这会给生产服务器带来不必要的负担。

## 创建量度

现在，您已具备分析所需的数据字段，接下来该查找或创建相关指标以构建您的分析。

在这里，您要执行以下计算：


`Time between a customer's registration date and first purchase date`&rbrack;的&#x200B;_&lbrack;总和/[注册并购买的客户总数]_

您希望看到根据客户的注册日期绘制的计算随时间变化或趋势。 以下是如何[在[!DNL Commerce Intelligence]中创建此量度](../../data-user/reports/ess-manage-data-metrics.md)：

1. 转到&#x200B;**[!UICONTROL Data]**&#x200B;并选择`Metrics`选项卡。
1. 单击&#x200B;**[!UICONTROL Add New Metric]**&#x200B;并选择`user`表（您在其中创建了上述维度）。
1. 从下拉列表中，选择按`Customer's registration date`列排序的`user`表中`Time between a customer's registration date and first purchase date`列的`Average`。
1. 添加任何相关的过滤器或过滤器集。

此量度现已准备就绪。

## 创建报告

设置了新量度后，您可以使用该量度报告注册到按注册日期列出的首次购买日期之间的平均时间。

只需转到任意仪表板，然后[使用上面创建的指标](../../data-user/reports/ess-manage-data-metrics.md)创建报告。

### `Visual Report Builder` {#visualrb}

[使用`Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md)是可视化数据的最简单方法。 如果您不熟悉SQL或者希望快速创建报告，则最好使用VisualReport Builder。 只需单击几下，即可在您的组织内添加指标、划分数据和创建报表。 此选项对于初学者和专家都是完美的，因为它不需要任何技术专业知识。

|  |  |
|--- |--- |
| **这非常适合于……** | **这不太适合……** |
|  — 所有级别的分析/技术体验<br> — 快速创建报告<br> — 创建要与其他用户共享的分析 |  — 需要SQL特定函数的分析<br> — 测试新列 — 计算列取决于初始数据填充的更新周期，而使用SQL创建的列则不依赖更新周期。 |

{style="table-layout:auto"}

### 报表描述和图像

#### 向报表添加描述

在创建与团队其他成员共享的报告时，Adobe建议添加描述，以便其他用户更好地了解您的分析。

1. 单击任何报告顶部的&#x200B;**[!UICONTROL i]**。
1. 在Word框中输入说明。
1. 单击&#x200B;**[!UICONTROL Save Description]**。

请参阅下文：

![图表说明](../../assets/Chart_Description.gif)

#### 将报表导出为图像

是否需要在演示文稿或文档中包含报告？ 任何报告都可以使用位于每个报告右上角的`Report Options`菜单另存为图像(PNG、PDF或SVG格式)。

1. 单击任何报表右上角的齿轮图标。
1. 从下拉列表中选择`Enlarge`。
1. 当报告放大时，单击报告右上角的&#x200B;**[!UICONTROL Download]**。
1. 从下拉列表中选择首选图像格式。 下载立即开始。

请参阅下文：

![](../../assets/exp-rep-as-image.gif)
