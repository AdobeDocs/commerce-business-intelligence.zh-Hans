---
title: 提高广告活动的ROI
description: 了解一些评估营销活动效果的不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# 广告活动和ROI

MBI让您轻松 [结合广告成本数据和收入数据](../../data-analyst/importing-data/integrations/google-adwords.md) 从数据库中。 这将帮助您确定哪些促销活动的ROI最高。 在本文中，我们探索了几种评估营销活动效果的不同方法。

## 先决条件

* 导入广告成本数据：
   * [连接 [!DNL Google AdWords] to [!DNL MBI]](../importing-data/integrations/google-adwords.md):这将自动同步 [!DNL Adwords] 支出 [!DNL MBI]
   * [上传其他广告成本数据](../importing-data/connecting-data/import-offline-ad-data.md):对于没有直接连接器的通道，建议使用 [!DNL MBI]
   * 如果您从多个来源导入成本数据，我们可以 [整合](../../best-practices/consolidating-your-tables.md) 中的数据 [!DNL MBI]. 简单 [提交支持票证](../../guide-overview.md).
* [跟踪用户获取渠道数据](../analysis/google-track-user-acq.md)

## 用户获取促销活动

针对用户获取的营销活动可以从多个角度进行衡量，包括：

1. 获取的营销活动新用户数
1. 营销活动从注册到购买的转化率
1. 基于平均用户生命周期值(LTV)的促销活动ROI

以上分析(1)和(2)将在 [识别热门营销渠道](../analysis/most-value-source-channel.md). 在此，我们探索分析(3)以衡量一段时间内的促销活动ROI。 这将回答从特定促销活动中获得的用户是否产生了足够的终身收入来支付其购买成本。

>[!NOTE]
>
>我们将假定所有促销活动成本都专门用于获取新用户。 实际上，您的促销活动成本也会与获取未转化的访问、重复购买者等共享。 但是，假设所有成本都用于获取新的注册用户，则最终的ROI将考虑最坏的情况（每次获取的最高成本），因此您可以确保实际ROI高于我们的计算。
>
>示例：假设您在一个促销活动上花费了20美元，该促销活动产生了10个新用户和10个重复购买者，则每个新用户的实际成本为$1，但根据我们的假设，购买新用户的所有成本都为$2，则每次购买的成本为$2。)

**1. 首先，创建一个图表以按促销活动划分广告成本：**

1. 创建 [!UICONTROL Metric] 你花的时间总和
1. 转到 [!UICONTROL Data > Metrics]
1. 选择 `Add New Metric` ，然后选择 [!DNL `Adwords...`] 正在记录您 [!DNL AdWords] 成本数据。
1. 在量度编辑器中，为您的量度指定一个名称(例如， [!UICONTROL AdWord Cost])
1. 使用下拉菜单，执行 **总和** 在 `adCost` 列 [!DNL Adwords...] 表（更改）按 `date` 列。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 我们完了。 单击 `Back to Metric List` ，然后转到任何功能板。

1. 创建按促销活动划分区段支出的报表
1. 在任何功能板中，单击 [!UICONTROL Add Report > Create new report]
1. 选择 [!UICONTROL Adword Cost] 我们刚刚创建的量度
1. 设置 [!UICONTROL Time period] to `All-time`和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 选项卡，添加 `campaign` as [!UICONTROL grouping field]，然后单击 `Add All` 框中。
1. 此报表将显示您的 [!DNL AdWords] 按促销活动成本

**2. 然后，我们将创建一个按促销活动计算新用户数的报表：**

1. 在任何功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 选择 `New users` 一个量度，用于计算一段时间内新注册用户的数量
1. 设置 [!UICONTROL Time period] to `All-time`和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 选项卡，添加 `campaign` as `grouping field`，然后单击 **`Add All`** 框中
1. 此报表将按营销活动显示您的所有注册用户

**3. 我们还可以创建一个报表，按促销活动划分平均用户LTV:**

1. 在任何功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 选择 `Average lifetime revenue` 计算平均用户生命周期收入的量度
1. 设置 [!UICONTROL Time period] to `All-time`和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 选项卡，添加 `campaign` 或 `utm\_campaign` as [!UICONTROL grouping field]，然后单击 `Add All` 框中
1. 此报表将按促销活动显示用户生命周期平均收入

**最后，我们将将这三个分析汇总到一份报告中，从而计算促销活动ROI:**

1. 在任何功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 添加作为输入，我们将使用上述三个量度。 每个人都将分配一封信件(例如\[`A`\], \[`B`\]和\[`C`\])
1. [!UICONTROL Cost]:添加量度AdWords成本 — 这将是变量\[A\]。 这只会按促销活动返回成本。
1. [!UICONTROL Users]:添加量度“新用户” — 此量度将为变量\[B\]。 这将只返回按营销活动划分的用户数。
1. [!UICONTROL LTV]:添加量度平均生命周期收入 — 此量度将为变量\[`C`\]。 这只需按营销活动返回LTV即可。

1. 单击“图表”旁边的隐藏图标，以便您能够集中在表格上
1. 现在我们将使用 `Add Formula` 要按如下方式组合这些量度：
1. [!UICONTROL ROI]:输入公式 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，如果\[`A`\]代表 `Ad Cost by Campaigns`, \[`B`\]代表 `New users by campaigns`和\[`C`\] `LTV by campaigns`. 这将返回（平均用户LTV — 每次客户获取的平均成本）/（每次客户获取的平均成本）的比率
1. [!UICONTROL Avg Return per User]:输入公式 **\[`C`\]-(\[`A`\]/\[`B`\])**. 这将返回通过计算（平均用户LTV） — （每次客户获取的平均成本）而对用户产生的平均利润。
1. [!UICONTROL CPA]:输入公式 **`\[A\]/\[B\]`**. 这将返回实际促销活动的每次获取成本。
1. 其他潜在的量度 [!DNL AdWords] 数据包括总和  `Impressions` 和 `adClicks` (从 [!DNL AdWords] 数据)，以及总计 `number of orders` 通过特定营销活动进行。
1. 根据用户注册或首次购买后的30天和90天的LTV计算ROI也许也很有趣。

1. 单击并拖动您的量度和公式可重新排序报表的列
1. 命名您的报表，并确保另存为表。

## 产品促销活动

您是否在运行特定于产品的广告？ 如果是，您可以通过计算特定产品的收入/成本来衡量这些促销活动的ROI。

>[!NOTE]
>
>我们将假定所有促销活动成本都专门用于生成特定产品的购买。 假设所有成本都花在了产生购买上，则最终的ROI将考虑最坏的情况（每次购买的最高成本），因此您可以确保实际ROI高于此计算。 示例：假设您在一个促销活动上花费了20美元，该促销活动产生了10个新用户和10次购买，则您的每次购买实际成本为$1，但根据我们假定所有购买新用户的成本都为$2，则每次购买的成本为$2。)*

在开始之前， [提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 将以下维度连接到行项目表(`sales\_flat\_order\_item, order\_item`):

* 订单的来源（如果您仅在用户级别跟踪反向链接来源，则加入用户的来源）
* 订购的促销活动（如果您仅在用户级别跟踪反向链接来源，则加入用户的促销活动）
* 订单的媒介（如果您仅在用户级别跟踪反向链接来源，则加入用户的媒介）

**1. 现在，首先创建一个图表，以返回特定产品的每个促销活动的收入：**

1. 在任何功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 选择 `Revenue by items` 在行项目级别计算收入的量度
1. 设置 [!UICONTROL Time period] to `All-time`和 [!UICONTROL Interval] to `None`
1. 在 `Filter by` 选项卡，添加 `product name 'IN'` 产品 `A`，产品 `B`，产品 `C`, ...&quot; 并包含营销活动所定向的所有产品名称(例如， `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. 在 `Group by` 选项卡，添加 `order's campaign` 或 `order's utm\_campaign` as `grouping` ，然后单击 **[!UICONTROL Add All]** 框中
1. 此报表将按促销活动显示特定产品的收入

**2. 为了计算ROI，我们将再次将多个量度组合到一个报表中：**

1. 在任何功能板中，单击 **[!UICONTROL Add Report > Create new report]**
1. 添加 `Revenue by items` 量度，按照过滤器和按营销活动中特定产品报表的指示进行分组，然后单击 **[!UICONTROL Hide]** 在量度的标量值之下
1. 现在，将 [!DNL AdWords Cost] 量度，按 `Ad cost by campaigns` 我们在 `User acquisition campaigns` 部分；然后单击 **[!UICONTROL Hide]** 在量度的标量值之下
1. 在实施这些量度后，我们现在将添加公式：
1. [!UICONTROL ROI]:输入公式 `\[A\]/\[B\]`，如果 `\[A\]` 表示 `Revenue per campaign for specific product(s)` 和 `\[B\]` 表示 `Ad cost by campaigns`. 这将返回（特定产品的收入）/（促销活动成本）的比率
1. [!UICONTROL Return]:输入公式 `\[A\]-\[B\]`. 这将返回通过计算（平均用户LTV） — （每次购买的平均成本）对用户产生的平均利润
1. （可选） [!UICONTROL Revenue]:取消隐藏 `Revenue by items` 用于查看每个促销活动中特定产品的收入的量度
1. （可选） [!UICONTROL Cost]:取消隐藏 `AdWords Cost` 量度以查看促销活动成本

1. 为报表提供一个名称，并确保将其另存为表

**3. 对每个广告的产品或产品组重复上述步骤1和2。**

## 相关文档

* [通过跟踪订单反向链接来源 [!DNL Google Analytics] 电子商务](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../analysis/track-usr-dev-browser.md)
* [发现最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [如何 [!DNL Google Analytics] UTM归因工作？](../analysis/utm-attributes.md)
* [在 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
