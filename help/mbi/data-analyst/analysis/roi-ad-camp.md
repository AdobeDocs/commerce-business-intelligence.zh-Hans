---
title: 提高广告促销活动的ROI
description: 了解评估营销活动性能的几种不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# 广告营销活动和ROI

[!DNL Adobe Commerce Intelligence] 让您轻松地 [将广告成本数据与收入数据相结合](../../data-analyst/importing-data/integrations/google-adwords.md) 从您的数据库中。 这有助于您确定哪些营销活动具有最高的投资回报(ROI)。 本主题探讨了评估促销活动性能的几种不同方法。

## 先决条件

* 导入您的广告成本数据：
   * [连接您的 [!DNL Google AdWords] 到 [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md)：这将同步您的 [!DNL Adwords] 支出 [!DNL Commerce Intelligence]
   * [上传其他广告成本数据](../importing-data/connecting-data/import-offline-ad-data.md)：对于没有直接连接器的通道，建议执行此操作 [!DNL Commerce Intelligence]
   * 如果从多个来源导入成本数据，则可以 [合并](../../best-practices/consolidating-your-tables.md) 中的数据 [!DNL Commerce Intelligence]. 简单 [提交支持服务单](../../guide-overview.md#Submitting-a-Support-Ticket).
* [跟踪用户获取渠道数据](../analysis/google-track-user-acq.md)

## 用户获取促销活动

针对用户获取的促销活动可以从多个角度进行衡量，包括：

1. 获得营销活动的新用户数
1. 从注册到购买营销活动的转化率
1. 基于平均用户生命周期值(LTV)的促销活动ROI

有关上述分析(1)和(2)的详情，请参阅以下主题的独立教程： [识别您的主要营销渠道](../analysis/most-value-source-channel.md). 在这里，您可以探索分析(3)来衡量一段时间内的促销活动ROI。 这可回答从特定营销活动获得的用户是否产生了足够的生命周期收入来覆盖收购成本。

>[!NOTE]
>
>此示例假定所有促销活动成本都专门用于获取新用户。 实际上，您的促销活动成本还与获得未转化访问次数、回头客等共用。 假设所有成本都用于获取新的注册用户，则生成的ROI将考虑最坏的情况（每次获取的最高成本）。 您可以确保您的实际ROI高于您的计算。
>
>示例：假设您在一个产生10个新用户和10个重复购买者的营销活动上花费了$20，则每个新用户的实际成本为$1。 但是，假设所有成本都花在了收购新用户上，那么每次收购的成本是2美元。

**1. 首先创建一个按促销活动划分广告成本的图表：**

1. 创建 [!UICONTROL Metric] 你花的时间总和
1. 转到 [!UICONTROL Data > Metrics]
1. 选择 `Add New Metric` 并选择 [!DNL `Adwords...`] 正在录制 [!DNL AdWords] 成本数据。
1. 在指标编辑器中，为您的指标提供一个名称(例如， [!UICONTROL AdWord Cost])
1. 使用下拉菜单执行 **总和** 在 `adCost` 中的列 [!DNL Adwords...] 表（更改），排序依据： `date` 列。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 单击 `Back to Metric List` 转到顶部的任何仪表板。

1. 创建按营销活动划分区段开支的报表
1. 在任意功能板中，单击 [!UICONTROL Add Report > Create report]
1. 选择 [!UICONTROL Adword Cost] 您刚刚创建的量度
1. 设置 [!UICONTROL Time period] 到 `All-time`、和 [!UICONTROL Interval] 到 `None`
1. 在 `Group by` 选项卡，添加 `campaign` 作为 [!UICONTROL grouping field]，然后单击 `Add All` 在盒子里。
1. 此报表可显示您的所有时间 [!DNL AdWords] 按营销活动列出的成本

**2. 创建一个按营销活动计数新用户的报表：**

1. 在任意功能板中，单击 **[!UICONTROL Add Report > Create report]**
1. 选择 `New users` 用于计算一段时间内新注册用户数的量度
1. 设置 [!UICONTROL Time period] 到 `All-time`、和 [!UICONTROL Interval] 到 `None`
1. 在 `Group by` 选项卡，添加 `campaign` 作为 `grouping field`，然后单击 **`Add All`** 在框中
1. 此报表按营销活动显示您的所有时间注册用户

**3. 创建一个报表，按营销活动对平均用户LTV进行分段：**

1. 在任意功能板中，单击 **[!UICONTROL Add Report > Create report]**
1. 选择 `Average lifetime revenue` 计算平均用户生命周期收入的量度
1. 设置 [!UICONTROL Time period] 到 `All-time`、和 [!UICONTROL Interval] 到 `None`
1. 在 `Group by` 选项卡，添加 `campaign` 或 `utm\_campaign` 作为 [!UICONTROL grouping field]，然后单击 `Add All` 在框中
1. 此报表可按营销活动显示您的平均用户生命周期收入

**最后，通过将以下三个分析汇总到一个报表中来计算促销活动ROI：**

1. 在任意功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 将添加为输入，然后使用上面使用的三个量度。 每个用户档案都分配有一个字母(例如，\[`A`\]， \[`B`\]和\[`C`\])
1. [!UICONTROL Cost]：添加AdWords成本量度 — 这是变量\[A\]。 按营销活动可返回成本。
1. [!UICONTROL Users]：添加指标“新用户” — 这是变量\[B\]。 这将返回按营销活动划分的用户数。
1. [!UICONTROL LTV]：添加量度平均生命周期收入 — 这是变量\[`C`\]。 这将按营销活动返回LTV。

1. 单击“图表”一字旁边的隐藏图标，以便集中在该表中
1. 现在使用 `Add Formula` 要组合这些量度，请执行以下操作：
1. [!UICONTROL ROI]：输入公式 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，如果\[`A`\]表示 `Ad Cost by Campaigns`， \[`B`\]表示 `New users by campaigns`，和\[`C`\] `LTV by campaigns`. 这会返回以下比率：（平均用户LTV — 每次购置的平均成本）/（每次购置的平均成本）
1. [!UICONTROL Avg Return per User]：输入公式 **\[`C`\]-(\[`A`\]/\[`B`\])**. 这将返回通过计算（平均用户LTV） — （每次购买的平均成本）得出的用户的平均利润。
1. [!UICONTROL CPA]：输入公式 **`\[A\]/\[B\]`**. 这将返回每次客户获取的实际营销活动成本。
1. 要从中包含的其他潜在量度 [!DNL AdWords] 数据包括  `Impressions` 和 `adClicks` (起始日期 [!DNL AdWords] data)，以及总计 `number of orders` 通过特定营销活动制作。
1. 在用户注册或首次购买后30天和90天根据LTV计算ROI可能也很有趣。

1. 您可以随时单击并拖动量度和公式，以重新排序报表中的列
1. 命名报告并确保另存为表。

## 产品营销活动

您是否运行特定于产品的广告？ 如果是这样，您可以通过计算特定产品的收入/成本来衡量这些促销活动的ROI。

>[!NOTE]
>
>此示例假设所有促销活动成本都专门用于生成特定产品的购买。 假设所有成本都花在生成购买上，则生成的ROI将考虑最坏的情况（每次购买的最高成本）。 您可以确保实际ROI高于此计算。 示例：假设您在一个产生10个新用户和10次购买的营销活动上花费了$20，则每次购买的实际成本为$1。 假设所有成本都花在了获取新用户上，则每次购买的成本为2美元。

开始之前， [提交支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 要将以下维度联接到行项目表(`sales\_flat\_order\_item, order\_item`)：

* 订单的来源（如果您仅在用户级别跟踪反向链接来源，则加入用户的来源）
* 订单的促销活动（如果您仅在用户级别跟踪反向链接来源，则加入用户的促销活动）
* 订单媒介（如果您仅在用户级别跟踪反向链接来源，则加入用户的媒介）

**1. 现在，首先创建一个图表，该图表返回特定产品的每个促销活动的收入：**

1. 在任意功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 选择 `Revenue by items` 计算行项目级别收入的量度
1. 设置 [!UICONTROL Time period] 到 `All-time`、和 [!UICONTROL Interval] 到 `None`
1. 在 `Filter by` 选项卡，添加 `product name 'IN'` 产品 `A`，产品 `B`，产品 `C`， ... ”并包含营销活动以逗号分隔的所有目标产品名称(例如， `product name 'IN' yellow t-shirt`， `red t-shirt, blue t-shirt`)
1. 在 `Group by` 选项卡，添加 `order's campaign` 或 `order's utm\_campaign` 作为 `grouping` 字段，然后单击 **[!UICONTROL Add All]** 在框中
1. 此报表按营销活动显示特定产品的收入

**2. 要计算ROI，请再次将指标合并到一个报表中：**

1. 在任意功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 添加 `Revenue by items` 量度，按照上述特定产品营销活动报表中的过滤器和分组说明进行筛选，然后单击 **[!UICONTROL Hide]** 在量度的标量值下方
1. 现在添加 [!DNL AdWords Cost] 量度，按照过滤器中的说明进行分组 `Ad cost by campaigns` 您在中探索的报告 `User acquisition campaigns` 部分，然后单击 **[!UICONTROL Hide]** 在量度的标量值下方
1. 设置好这些量度后，添加公式：
1. [!UICONTROL ROI]：输入公式 `\[A\]/\[B\]`，如果 `\[A\]` 表示 `Revenue per campaign for specific product(s)` 和 `\[B\]` 表示 `Ad cost by campaigns`. 这会返回（特定产品的收入）/（促销活动成本）的比率
1. [!UICONTROL Return]：输入公式 `\[A\]-\[B\]`. 通过计算（平均用户LTV） — （每次客户获取的平均成本），这会返回用户的平均利润
1. （可选） [!UICONTROL Revenue]：取消隐藏 `Revenue by items` 量度以查看每个营销活动的特定产品的收入
1. （可选） [!UICONTROL Cost]：取消隐藏 `AdWords Cost` 用于查看营销活动成本的量度

1. 为报表命名，并确保将其另存为表

**3. 对每个广告的产品或产品组重复上述步骤1和2。**

## 相关文档

* [通过以下方式跟踪订单反向链接来源： [!DNL Google Analytics] 电子商务](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../analysis/track-usr-dev-browser.md)
* [了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接您的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [如何 [!DNL Google Analytics] UTM归因工作？](../analysis/utm-attributes.md)
* [在中进行UTM标记的五个最佳实践 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
