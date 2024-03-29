---
title: Google Analytics中的UTM跟踪
description: 了解Google Analytics中UTM跟踪（标记）的最佳实践。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM跟踪

`UTM` 跟踪是一种URL标记约定，它使您能够分析用户的来源。 如果您查看在大多数营销电子邮件或横幅广告中单击的URL，则会看到UTM标记。 正是这些长链接以如下内容结尾 `utm\_source` 和 `utm\_medium`.

[!DNL Google Analytics] 用途 `UTM` 标记以了解流量的来源。 这些信息部分来自 [HTTP反向链接](https://en.wikipedia.org/wiki/HTTP_referer) 但剩下的东西你得给自己提供 `UTM` 参数。 当您看到 `google adwords` 或 `email marketing`，表示这些 `UTM` 通过单击原始链接进行记录，然后存储在用户的Cookie中的参数。 从那里， [!DNL Google Analytics] 使用该数据 [属性兴趣行为](../data-analyst/analysis/google-track-user-acq.md) 在您的网站上。 了解这些参数的用途有助于您了解如何以最佳方式设置和使用UTM标记。

## UTM标记的最佳实践

下面列出了使用设置URL时要记住的五大要点 `UTM` 标记。

### 1.旨在标记您可以控制的每个访问您网站的URL

每次要求用户单击链接时，您都应设置 `UTM` 标记。 这包括您的所有电子邮件链接（您的电子邮件服务提供商可能会自动标记您的URL）、广告链接、新闻文章、博客文章。

### 2.使用工具创建URL

`UTM` — 标记的URL可能会很麻烦。 不要试图在长时间内键入它们，而要使用工具 [象这样](https://support.google.com/analytics/answer/1033867?hl=en) 帮助你。 这可确保您考虑向URL添加所有合理的参数，并且您会从该URL中直接获得要复制粘贴的URL。 要管理社交链接，请使用 [!DNL Hootsuite] 包含用于将自定义URL参数添加到所有链接的选项。

### 3.确保参数值区分大小写

请务必记住，标记 `utm\_source=adwords` 是与不同的标记 `utm\_source=Adwords`. 考虑将所有内容变为小写。

### 4.将UTM参数值存储在数据库中

每次发生交易或事件时，您都要评估营销活动的效果。 为此，可以从 [[!DNL Google Analytics] 将Cookie导入数据库](../data-analyst/analysis/google-track-user-acq.md).

### 5.考虑如何命名营销活动

为了跟踪营销工作如何随时间的推移而改善，您需要对命名惯例保持警惕。 保持简单，并尽可能减少工作量。 复杂的命名系统更难维护。

在数据库中捕获这些数据后，您可以通过更复杂的分析来评估营销和广告的表现，包括 [客户存留期值](../data-analyst/analysis/ess-expected-ltv.md)， [重复购买率](../data-analyst/analysis/repurchase-behavior.md)、和 [平均订单价值](../data-analyst/analysis/basic-analytics.md).
