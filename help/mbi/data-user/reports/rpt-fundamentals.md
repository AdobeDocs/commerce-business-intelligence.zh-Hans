---
title: 使用报表
description: 了解如何使用报表数据。
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 使用报告

在中使用报表 [!DNL MBI] 帮助您回答业务问题 — 是只想查看本月与上一年的收入对比，还是想了解您最新的购置成本 [!DNL Google AdWords] 营销活动。

从问题到答案的路径到底是什么样的？

为了帮助您可视化此过程，该路由如下图所示。 本主题说明了如何解决分析问题，以及获取所需数据所需的后端后勤工作。

## 从问题开始

您知道，为了改善您的业务，您不断提出各种问题，从提高客户满意度到降低供应成本。 您专注于如何将您的问题转化为有助于您制定决策的分析。

对于此示例，假设您要回答以下问题：

* 我的新注册者的转化速度如何？

## 识别测量

现在应该确定一系列可能的分析和衡量标准，以帮助回答这个问题。 对于此示例，请重点关注以下量度：

* 每次使用从注册到首次购买日期的平均时间。

这揭示了注册日期与用户的首次购买日期之间经过的平均时间，并提供了有关用户在转化漏斗中的这最后一步如何表现的想法。

## 查找数据

了解如何衡量只有我们才能获得其中一部分机会。 要评估每位用户从注册到首次购买日期的平均时间，您需要确定由衡量标准组成的所有数据点。

将度量划分为其核心组件。 您必须知道已注册的人数，或注册的人数，已购买的人数，以及两次事件之间经过的时间。

在更高级别上，您需要知道在数据库中从何处查找此数据，特别是：

* 每次有人注册时记录一行数据的表
* 记录每次有人购买时的数据行的表
* 可用于连接或引用 `purchase` 表 `customer` 表 — 这允许我们了解谁购买了

在更精细的粒度级别，您需要确定用于此分析的确切数据字段：

* 包含客户注册日期的数据表和列：例如 `user.created\_at`
* 包含购买日期的数据表和列：例如 `order.created\_at`

## 创建数据列以供分析

除了上面列出的本机数据列之外，还需要一组计算的数据字段来启用此分析，包括：

* `Customer's first purchase date` 返回特定用户的 `MIN(order.created_at`)

然后用于创建：

* `Time between a customer's registration date and first purchase date`，返回从注册到首次购买日期之间经过的特定用户时间。 这是稍后量度的基础。

这两个字段都需要在用户级别创建(例如，在 `user` 表)。 这使得平均分析可以由用户标准化（换句话说，此平均计算中的分母是用户计数）。

这里是 [!DNL MBI] 步入！ 您可以使用 [!DNL MBI] 创建上述列的Data warehouse。 请联系Adobe分析团队，向我们提供用于创建的新列的特定定义。 您还可以使用 [列编辑器](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

最佳做法是避免直接在数据库中创建这些计算数据字段，因为它会给生产服务器带来不必要的负担。

## 创建量度

现在，您已具备分析所需的数据字段，接下来该查找或创建相关指标以构建您的分析。

在此处，您要执行以下计算：


_[总和 `Time between a customer's registration date and first purchase date`] / [注册和购买的客户总数]_

您希望根据客户的注册日期，查看此计算随时间绘制的图或趋势图。 下面是如何 [创建此量度](../../data-user/reports/ess-manage-data-metrics.md) 在 [!DNL MBI]：

1. 转到 **[!UICONTROL Data]** 并选择 `Metrics` 选项卡。
1. 单击 **[!UICONTROL Add New Metric]** 并选择 `user` 表（您创建上述维的位置）。
1. 从下拉菜单中，选择 `Average` 在`Time between a customer's registration date and first purchase date` 中的列 `user` 表排序方式 `Customer's registration date`  列。
1. 添加任何相关的过滤器或过滤器集。

此量度现已准备就绪。

## 创建报告

设置了新量度后，您可以使用该量度按注册日期报告注册与首次购买日期之间的平均时间。

只需转到任意仪表板并 [创建报告](../../data-user/reports/ess-manage-data-metrics.md) 使用上面创建的量度。

### `Visual Report Builder` {#visualrb}

[此 `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) 是可视化数据的最简单方法。 如果您不熟悉SQL或希望快速创建报告，则最好使用可视化Report Builder。 只需单击几下，您就可以添加指标、划分数据并创建报告以将其添加到整个组织中。 此选项对于初学者和专家都是完美的，因为它不需要任何技术专业知识。

|  |  |
|--- |--- |
| **这个很适合……** | **这个不太适合……** |
|  — 所有级别的分析/技术经验<br> — 快速创建报告<br> — 创建要与其他用户共享的分析 |  — 需要SQL特定函数的分析<br> — 测试新列 — 计算列取决于初始数据填充的更新周期，而使用SQL创建的列则不然。 |

{style="table-layout:auto"}

### 报表说明和图像

#### 向报表添加描述

在创建与您团队的其他成员共享的报告时，Adobe建议添加描述，以便其他用户更好地了解您的分析。

1. 单击 **[!UICONTROL i]** 位于任何报表的顶部。
1. 在单词框中输入描述。
1. 单击 **[!UICONTROL Save Description]**.

请参阅下文：

![图表描述](../../assets/Chart_Description.gif)

#### 将报表导出为图像

是否需要在演示文稿或文档中包含报告？ 任何报告都可以使用另存为图像(PNG、PDF或SVG格式) `Report Options` 菜单，位于每个报告的右上角。

1. 单击任何报表右上角的齿轮图标。
1. 从下拉菜单中，选择 `Enlarge`.
1. 当报表放大时，单击 **[!UICONTROL Download]** 报表的右上角。
1. 从下拉列表中选择首选的图像格式。 下载立即开始。

请参阅下文：

![](../../assets/exp-rep-as-image.gif)
