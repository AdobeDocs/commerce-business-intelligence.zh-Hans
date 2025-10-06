---
title: Report Builder同类群组
description: 了解对在生命周期内具有相似特征的用户组的分析。
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Report Builder同类群组

您是否曾想过研究用户的不同子集在一段时间内的行为？ 例如，您是否曾想知道，在促销期间注册的用户平均终生收入是否比没有注册的用户高？ 如果答案是`Yes`，则`Cohort Report Builder`是您的最佳工具。 [!DNL Adobe Commerce Intelligence]已优化为执行此分析，并使其与您的业务相关。

## 什么是同类群组分析？ {#what}

`Cohort`分析可以宽泛地定义为分析在其生命周期内具有相似特征的用户组。 它允许您识别不同用户群组中的行为趋势。

有关`cohort`分析的深入入门课程，请查阅[此页面](https://www.cohortanalysis.com/)。

在您的[!DNL Commerce Intelligence]仪表板中，可以轻松根据帐户中的`cohorts`日期和量度创建用户`cohort`。

## 为什么同类群组分析很重要？ {#important}

如上所述，`cohort`分析允许您识别不同用户组之间的行为趋势。 通过深入了解特定组的行为，您可以定制您的决策和支出以最大限度地提高您的销售额。 例如，进行生命周期收入`cohort`分析 — 尽管这种分析由于多种原因而很有用，但直接分析是更好的客户获取决策。

## 如何创建我自己的`cohort`分析？

### 新架构

以下是在`Cohort Report Builder`新架构[上使用](../../administrator/account-management/new-architecture.md)的说明。

1. 在左侧选项卡上单击&#x200B;**[!UICONTROL Report Builder]**，或在任意仪表板中单击&#x200B;**[!UICONTROL Add Report** > **Create Report]**。

1. 在`Report Builder`选择屏幕中，单击&#x200B;**[!UICONTROL Create Report]**&#x200B;选项旁边的`Visual Report Builder`。

**添加指标**

现在您位于`Report Builder`中，添加要对其执行分析的量度（示例： `Revenue`或`Orders`）。

>[!NOTE]
>
>本机[!DNL Google Analytics]量度与`Cohort Report Builder`不兼容。

**将指标视图切换为`Cohort`**

![可视化Report Builder显示同类群组分析切换选项](../../assets/visual-report-builder-cohort-toggle.png)

这将打开一个新窗口来配置`Cohort`报告的详细信息。

### 生成`Cohort`报告需要五个规范：

1. 如何对`cohorts`分组
1. `cohort`时段
1. 要查看的`cohorts`的数量
1. 每个`cohort`必须包含的最小数据量
1. `cohort`发生次数之后的时间范围

#### 1.分组`cohorts`

`Cohorts`按时间戳分组，如&#x200B;**注册日期**&#x200B;或&#x200B;**首次订购日期**。

>[!NOTE]
>
>您不能使用针对`cohort`日期生成量度的相同时间戳。 对于需要此功能的分析，您可以改用`Standard report builder`。

#### &#x200B;2. `Cohort`时段

选择对`cohorts`进行分组所依据的时间段。 换句话说，您在上面选择的时间戳的哪一部分最重要；`week`、`month`、`quarter`或`year`？ 您的报表以您在此处选择的任意间隔显示数据

#### 3.和4. 设置要查看的`cohorts`的数目以及每个`cohort`必须拥有的数据量

这些参数可帮助您仅查看感兴趣的`cohorts`，并且窗口底部的方便的`Preview`框准确地显示了报表中显示的同类群组。

默认情况下，不包括当前`cohort`，除非您将每个`cohort`所需的最小数据量更改为`0`。 在这种情况下，当前时间段的`cohort`仅包括部分数据。

#### 5.发生`Cohort`次之后的时间范围

此功能允许您为所选`cohorts`设置查看数据的时间范围。 例如，如果您要根据`cohorts`查看24个月的月度`customer's first order date`，但您只对每个`cohort`的前3个月的数据感兴趣，则可以将`number of cohorts to view`设置为`24`，将`time range after cohort occurrence`设置为`3`。

此值的间隔随您在`cohort time period`中选择的任何内容而更改，该值默认设置为`12`；除非单击日历图标对其进行编辑，否则该值不会更改。

![显示日期选项的同类群组时间范围选择器](../../assets/cohort-time-range.png)

#### 其他注释

* [!UICONTROL Filters]：当您在`Standard`和`Cohort`视图之间切换时，应用于您的量度的保持不变。

* 请参阅[`Perspectives`](#perspectives)。

#### 示例

下面是一个将所有这些结合在一起的示例。 在此示例中，我想查看`cohort`首次购买后的订单行为，以查看该同类群组是否会在未来6个月内再次进行重复购买。

![订单同类群组](../../assets/crb_example.gif)

### 旧式架构

#### 旧式架构 {#personalinfo}

以下是特定于`Cohort Report Builder`旧版本的说明。 如果您有兴趣使用新版本，请参阅[新架构](../../administrator/account-management/new-architecture.md)以了解有关迁移到[!DNL Commerce Intelligence]新架构帐户的更多信息。

#### 如何创建我自己的`cohort`分析？ {#create}

![使用配置选项创建同类群组分析对话框](../../assets/create-cohort-analysis.png)

`Cohort`分析正在进行中！ 在这里，您可以看到收入在一段时间内以累计和每个用户为单位增长。

本节将指导您创建自己的`cohort`分析。 有关示例（以及演示该过程的动画GIF），请查看本主题的[示例部分](#examples)。

1. 在左侧选项卡上单击&#x200B;**[!UICONTROL Report Builder]**，或在任意仪表板中单击&#x200B;**[!UICONTROL Add Report** > **Create Report]**。

1. 在`Report Builder Selection`屏幕中，单击&#x200B;**[!UICONTROL Create Report]**&#x200B;选项旁边的`Cohort Analysis`。

#### 添加量度

现在您位于`Cohort Report Builder`中，添加要对其执行分析的量度（示例： `Revenue`或`Number of orders`）。

>[!NOTE]
>
>本机[!DNL Google Analytics]量度与`Cohort Report Builder`不兼容。

#### 选择同类群组日期 {#date}

下一步是指定`cohort date`。 这是对您的用户进行分组的日期。 例如，可能是`User's first order date`或`User's registration date`。

>[!NOTE]
>
>您不能将生成量度的日期与`created at`一起使用（例如： `cohort date`）。

#### 设置间隔和时间段

接下来，设置`Interval`和`Time Period`。

`Interval`
`Interval`选项允许您设置`length`的`cohorts`。 例如，如果将此值设置为`Month`，则报表将以月为单位进行测量。

您可以使用&#x200B;**持续时间**&#x200B;菜单更改这些间隔在x轴上的显示方式。

`Time Period`
使用`Time Period`菜单选择要分析的特定用户`cohorts`。 您可以每`cohort`显示一次，从列表中选择一次，指定时间范围，或定义要包括的`cohorts`滚动时间范围。 例如，如果您使用了`Specific Cohorts`选项，则可以选择要包含在分析中的特定月份：

![使用`Time Period`菜单添加特定`Cohorts`](../../assets/Cohort_Time_Period.gif)

如果您按注册日期对您`cohorts`进行分组，然后在`Specific Cohorts`列表中选择四月、五月和六月，则将包含这些月份中注册的任何用户。

#### 定义X轴

在`duration`下，您可以定义图表的X轴设置。 即，每个数据点表示的时间段数，以及分析中包含的数据点数。

#### 选择`counting members`表

如果您选择按从另一个表中加入的`cohort date`对用户进行分组，则可能会看到`counting members in the … table`选项。

![显示独立模式和累积模式的同类群组计数成员选项](../../assets/Cohort_Counting_Members_option.png)

请查看示例以了解此设置。 假设您按`Revenue`构建了`Customer's registration date`量度同类群组报表。 您还需要使用透视`Average value per cohort member`来查看一段时间中每位购买者的收入。 要确定每个购买者的平均价值，您需要确定要除以的购买者数量。 是您`customers`表中的已注册客户数，还是您`orders table`中相同期间的不同购买者的数量？

此设置回答该问题。 对`customers`表中的成员进行计数将平均包括所有客户（无论他们是否进行了购买）。 对`orders`表中的成员进行计数只包括购买过的客户。

#### 选择透视 {#perspective}

定义量度以及要如何分析该量度后，可以选择要使用的`perspective`。

报表可视化图表上方是`perspective`设置的下拉列表。

查看[透视](#perspectives)。

![显示不同视图选项的“同类群组透视”菜单](../../assets/Cohort_Perspective_Menu.png)

## 同类群组分析示例 {#examples}

现在您已了解如何创建`cohort`分析，请查看一些示例。

### 我想了解我的用户`cohorts`如何随时间的推移不断增长。

![用户`cohorts`随时间增长](../../assets/cohort1.gif)

在此示例中，您分析了`Revenue`量度，按`customer's first order date`对同类群组进行了分组，并选择了要包含在分析中的8个最新`cohorts`（在`Time Period`菜单中定义）。 要查看同类群组随时间的增长情况，您使用了`Cumulative Average Value per Cohort Member` `perspective`。

### 我想知道，平均而言，一个用户在其一生中的不同时刻下了多少订单。

(../../assets/cohort2.gif

在此示例中，您分析了`Number of orders`量度，按`customer's first order date`对您的同类群组进行了分组，并在分析中包含了最近的8个同类群组（在`Time Period`菜单中定义）。 要查看每个同类群组的平均订单数，您已将`perspective`更改为`Average Value per Cohort Member`。

### 我想了解用户的未来购买活动与他们在业务中的第一个月活动有何不同。

![将用户的未来购买活动与其第一个月的活动进行比较](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
这显示了给定同类群组在其生命周期的任何给定点上的增量贡献。 （示例：“第6周”点显示用户在其第六周提出的所有数据点。）

`Average Value per Cohort Member`
这将`Standard cohort`分析以(1)除以每个`cohort`组中的用户数。 这对于根据苹果对苹果来比较同类群组性能非常有用，因为并非所有同类群组都可能包含相同数量的用户。 例如，来自特定`cohort`的每位用户平均第6周收入。

`Cumulative`
此`perspective`显示基于`cohort`的传统`cumulative`分析。 换句话说，它显示了给定同类群组在生命周期中任何给定时间至今的总贡献。 例如，某个同类群组中用户连续六周后的累计收入。

`Cumulative Average Value per Cohort Member`
这会将(3)中的`Cumulative`分析除以每个`cohort`组中的用户数。 它显示`cohort`生命中每个期间每个`cohort's`成员的平均生命周期贡献（通常为平均生命周期收入）。 例如，6月份加入的用户在六个月后的平均生命周期收入。

`Percent of First Value (show first value)`
这会分析`cohort`生命周期中特定时间的聚合`cohort's`贡献占其第一个周期中贡献的百分比。 例如，第6个月收入除以在6月加入的用户的第1个月收入。

`Percent of First Value (hide first value)`
这与上述`perspective`相同，不同之处在于隐藏了第一个时间段值100%。

## 正在结束 {#finish}

`Cohort Report Builder`已针对按公共`cohort date`对用户进行分组进行了优化。 您可能希望按类似的活动或属性对用户进行分组。 Adobe建议退出[此关于定性同类群组](../dev-reports/create-qual-cohort-analysis.md)的教程以开始。
