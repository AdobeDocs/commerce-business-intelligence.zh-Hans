---
title: 提高广告促销活动的ROI
description: 了解评估营销活动性能的几种不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Advertising促销活动和ROI

[!DNL Adobe Commerce Intelligence]允许您从数据库中[将广告成本数据和收入数据](../../data-analyst/importing-data/integrations/google-adwords.md)轻松合并。 这有助于您确定哪些营销活动具有最高的投资回报(ROI)。 本主题探讨了评估活动性能的几种不同方法。

## 先决条件

* 导入您的广告成本数据：
   * [将您的 [!DNL Google AdWords] 连接到 [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md)：这将同步您的[!DNL Adwords]在[!DNL Commerce Intelligence]中的花费
   * [上载其他广告成本数据](../importing-data/connecting-data/import-offline-ad-data.md)：建议对没有直接连接到[!DNL Commerce Intelligence]的渠道执行此操作
   * 如果从多个来源导入成本数据，则可以[合并](../../best-practices/consolidating-your-tables.md)在[!DNL Commerce Intelligence]中的数据。 只需[提交支持票证](../../guide-overview.md#Submitting-a-Support-Ticket)。
* [跟踪用户获取渠道数据](../analysis/google-track-user-acq.md)

## 用户获取促销活动

可从多个角度衡量针对用户获取的促销活动，包括：

1. 获得营销活动的新用户数
1. 从注册到购买营销活动的转化率
1. 基于平均用户生命周期值(LTV)的促销活动ROI

在关于[确定您的主要营销渠道](../analysis/most-value-source-channel.md)的独立教程中，将探讨上述分析(1)和(2)。 在这里，您可以探索分析(3)以衡量一段时间内的促销活动ROI。 此量度可回答从特定营销活动购买的用户是否产生了足够的生命周期收入以覆盖购买成本。

>[!NOTE]
>
>此示例假设所有促销活动成本都专门用于获取新用户。 实际上，您的促销活动成本还会与获得未转化访问次数、回头客等共用。 假设所有成本都用于获取新的注册用户，则生成的ROI将考虑最坏的情况（每次获取成本最高）。 您可以确保您的实际ROI高于您的计算。
>
>示例：假设您在一个产生10个新用户和10个重复购买者的营销活动上花费了$20，则每个新用户的实际成本为$1。 但是，假设所有成本都花在了收购新用户上，那么每次收购的成本是2美元。

**1. 首先，创建一个按促销活动划分广告成本的图表：**

1. 创建一段时间内您的总支出的[!UICONTROL Metric]
1. 转到[!UICONTROL Data > Metrics]
1. 选择`Add New Metric`并选择正在记录[!DNL `Adwords...`]成本数据的[!DNL AdWords]表。
1. 在指标编辑器中，为您的指标提供一个名称（例如，[!UICONTROL AdWord Cost]）
1. 使用这些下拉列表，对按&#x200B;**列排序的**&#x200B;表（更改）中的`adCost`列执行[!DNL Adwords...]Sum`date`。
   添加新量度后显示![成功消息](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 单击顶部的`Back to Metric List`并转到任意仪表板。

1. 创建按营销活动划分区段的报表
1. 在任意仪表板中，单击[!UICONTROL Add Report > Create report]
1. 选择您刚刚创建的[!UICONTROL Adword Cost]量度
1. 将[!UICONTROL Time period]设置为`All-time`，将[!UICONTROL Interval]设置为`None`
1. 在`Group by`选项卡下，将`campaign`添加为[!UICONTROL grouping field]，然后在框中单击`Add All`。
1. 此报表按营销活动显示您的全时[!DNL AdWords]成本

**2。 创建按营销活动计数新用户的报告：**

1. 在任意仪表板中，单击&#x200B;**[!UICONTROL Add Report > Create report]**
1. 选择计算一段时间内新注册用户数的`New users`指标
1. 将[!UICONTROL Time period]设置为`All-time`，将[!UICONTROL Interval]设置为`None`
1. 在`Group by`选项卡下，将`campaign`添加为`grouping field`，然后在框中单击&#x200B;**`Add All`**
1. 此报表可按营销活动显示您的所有时间注册用户

**3。 创建按促销活动划分平均用户LTV的报表：**

1. 在任意仪表板中，单击&#x200B;**[!UICONTROL Add Report > Create report]**
1. 选择用于计算平均用户生命周期收入的`Average lifetime revenue`量度
1. 将[!UICONTROL Time period]设置为`All-time`，将[!UICONTROL Interval]设置为`None`
1. 在`Group by`选项卡下，添加`campaign`或`utm\_campaign`作为[!UICONTROL grouping field]，然后单击框中的`Add All`
1. 此报表可显示按营销活动划分的平均用户生命周期收入

**最后，通过将这三项分析汇总到一个报告中来计算促销活动ROI：**

1. 在任意仪表板中，单击&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 添加作为输入，使用上面使用的三个量度。 为每个用户分配了一个字母（例如，\[`A`\]、\[`B`\]和\[`C`\]）
1. [!UICONTROL Cost]：添加指标AdWords成本 — 这是变量\[A\]。 按促销活动列出的退货成本。
1. [!UICONTROL Users]：添加量度“新用户” — 这是变量\[B\]。 这将返回按营销活动划分的用户数。
1. [!UICONTROL LTV]：添加量度平均生命周期收入 — 这是变量\[`C`\]。 这将按营销活动返回LTV。

1. 单击“图表”一字旁边的隐藏图标，以便集中查看表格
1. 现在使用`Add Formula`组合这些指标，如下所示：
1. [!UICONTROL ROI]：输入公式`(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，如果\[`A`\]表示`Ad Cost by Campaigns`，\[`B`\]表示`New users by campaigns`，\[`C`\] `LTV by campaigns`。 这会返回以下比率：（平均用户LTV — 每次购置的平均成本）/（每次购置的平均成本）
1. [!UICONTROL Avg Return per User]：输入公式&#x200B;**\[`C`\]-(\[`A`\]/\[`B`\])**。 通过计算（平均用户LTV） — （每次购买的平均成本），返回用户的平均利润。
1. [!UICONTROL CPA]：输入公式&#x200B;**`\[A\]/\[B\]`**。 这将返回实际营销活动的每次购置成本。
1. 要从[!DNL AdWords]数据包含的其他潜在量度包括`Impressions`和`adClicks`（来自[!DNL AdWords]数据）的总和，以及通过特定营销活动创建的总`number of orders`。
1. 在用户注册或首次购买后30天和90天根据LTV计算ROI可能也很有趣。

1. 您可以随时单击并拖动量度和公式，以重新排序报表中的列
1. 命名报告并确保另存为表。

## 产品营销活动

您是否在运行产品特定广告？ 如果是这样，您可以通过计算特定产品的收入/成本来衡量这些促销活动的ROI。

>[!NOTE]
>
>此示例假设所有促销活动成本都专门用于生成特定产品的购买。 假设所有成本都花费在生成购买上，则生成的ROI将考虑最坏的情况（每次购买的最高成本）。 您可以确保实际ROI高于此计算。 示例：假设您在一个产生10个新用户和10次购买的营销活动上花费$20，则每次购买的实际成本为$1。 假设所有成本都花在了获取新用户上，则每次购买的成本为2美元。

开始之前，[提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以将以下维度联接到行项目表(`sales\_flat\_order\_item, order\_item`)：

* 订单的来源（如果您仅在用户级别跟踪反向链接来源，则加入用户的来源）
* 订单的促销活动（如果您仅在用户级别跟踪反向链接来源，则加入用户的促销活动）
* 订单媒介（如果您仅在用户级别跟踪反向链接来源，则加入用户的媒介）

**1. 现在，首先创建一个图表，该图表返回特定产品的每个促销活动的收入：**

1. 在任意仪表板中，单击&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 选择在行项目级别计算收入的`Revenue by items`指标
1. 将[!UICONTROL Time period]设置为`All-time`，将[!UICONTROL Interval]设置为`None`
1. 在`Filter by`选项卡下，添加`product name 'IN'`产品`A`、产品`B`、产品`C`...&quot;，并包含营销活动以逗号分隔的所有产品名称（例如，`product name 'IN' yellow t-shirt`、`red t-shirt, blue t-shirt`）
1. 在`Group by`选项卡下，添加`order's campaign`或`order's utm\_campaign`作为`grouping`字段，然后单击框中的&#x200B;**[!UICONTROL Add All]**
1. 此报表可按营销活动显示特定产品的收入

**2。 要计算ROI，请再次将指标合并到一个报表中：**

1. 在任意仪表板中，单击&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 按照上面特定产品报表的营销活动中的过滤器和分组说明添加`Revenue by items`量度，然后单击量度标量值下方的&#x200B;**[!UICONTROL Hide]**
1. 现在，按照您在上面[!DNL AdWords Cost]部分中探索的`Ad cost by campaigns`报表中的筛选器和分组说明添加`User acquisition campaigns`指标；然后单击指标标量值下方的&#x200B;**[!UICONTROL Hide]**
1. 设定好这些量度后，添加公式：
1. [!UICONTROL ROI]：输入公式`\[A\]/\[B\]`，如果`\[A\]`表示`Revenue per campaign for specific product(s)`，`\[B\]`表示`Ad cost by campaigns`。 这会返回（特定产品的收入）/（促销活动成本）的比率
1. [!UICONTROL Return]：输入公式`\[A\]-\[B\]`。 通过计算（平均用户LTV） — （每次购买的平均成本），返回用户的平均利润
   1. （可选） [!UICONTROL Revenue]：取消隐藏`Revenue by items`量度以查看每个营销活动的特定产品的收入
   1. （可选） [!UICONTROL Cost]：取消隐藏`AdWords Cost`量度以查看营销活动的成本

1. 为报表命名，并确保将其另存为表

**3。 对每个广告的产品或产品组重复上述步骤1和2。**

## 相关文档

* [通过 [!DNL Google Analytics] E-Commerce跟踪订单反向链接来源](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../analysis/track-usr-dev-browser.md)
* [了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接你的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [ [!DNL Google Analytics] UTM归因如何工作？](../analysis/utm-attributes.md)
* [ [!DNL Google Analytics]中UTM标记的五个最佳实践](../../best-practices/utm-tagging-google.md)
