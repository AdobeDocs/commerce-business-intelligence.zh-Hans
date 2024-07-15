---
title: Google Analytics中的UTM跟踪
description: 了解Google Analytics中UTM跟踪（标记）的最佳实践。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM跟踪

`UTM`跟踪是URL的标记约定，它使您能够分析用户的来源。 如果您查看在大多数营销电子邮件或横幅广告中单击的URL，则会看到UTM标记。 是那些以`utm\_source`和`utm\_medium`之类的内容结尾的长链接。

[!DNL Google Analytics]使用`UTM`标记来了解流量的来源。 此信息中有些来自[HTTP反向链接](https://en.wikipedia.org/wiki/HTTP_referer)，但其余部分必须提供`UTM`参数。 当您看到`google adwords`或`email marketing`时，这意味着从原始链接点击中记录的这些`UTM`参数，然后存储在用户的Cookie中。 从那里，[!DNL Google Analytics]使用该数据来[归因您网站上的有趣行为](../data-analyst/analysis/google-track-user-acq.md)。 了解这些参数的用途有助于您了解如何以最佳方式设置和使用UTM标记。

## UTM标记的最佳实践

下面列出了使用`UTM`标记设置URL时要记住的五大要点。

### 1.旨在标记您可以控制的每个访问您网站的URL

每次要求用户单击链接时，您都应设置`UTM`标记。 这包括您的所有电子邮件链接（您的电子邮件服务提供商可能会自动标记您的URL）、广告链接、新闻文章、博客文章。

### 2.使用工具创建URL

`UTM`标记的URL可能会很麻烦。 请使用类似于[的工具](https://support.google.com/analytics/answer/1033867?hl=en)来帮助您，而不是尝试键入它们。 这可确保您考虑向URL添加所有合理的参数，并且您会从该URL中直接获得要复制粘贴的URL。 为了管理社交链接，诸如[!DNL Hootsuite]之类的工具包括向所有链接添加自定义URL参数的选项。

### 3.确保参数值区分大小写

请务必记住，标记`utm\_source=adwords`与`utm\_source=Adwords`是不同的标记。 考虑将所有内容变为小写。

### 4.将UTM参数值存储在数据库中

每次发生交易或事件时，您都要评估营销活动的效果。 为此，您可以将[[!DNL Google Analytics] Cookie中的UTM参数值读入数据库](../data-analyst/analysis/google-track-user-acq.md)。

### 5.考虑如何命名营销活动

为了跟踪营销工作如何随时间的推移而改善，您需要对命名惯例保持警惕。 保持简单，并尽可能减少工作量。 复杂的命名系统更难维护。

在数据库中捕获此数据后，您可以通过更复杂的分析来评估营销和广告的性能，包括[客户存留期值](../data-analyst/analysis/ess-expected-ltv.md)、[重复购买率](../data-analyst/analysis/repurchase-behavior.md)和[平均订单值](../data-analyst/analysis/basic-analytics.md)。
