---
title: UTM跟踪Google Analytics
description: 了解Google Analytics中UTM跟踪（标记）的最佳实践。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# UTM跟踪

`UTM` 跟踪是URL的标记约定，可让您分析用户的来源。 如果您查看从大多数营销电子邮件或横幅广告中单击的URL，将会看到UTM标记。 是那些长链条，以这类事件结尾 `utm\_source` 和 `utm\_medium`.

[!DNL Google Analytics] 使用 `UTM` 标记以了解流量的来源。 其中一些信息来自 [HTTP引用](https://en.wikipedia.org/wiki/HTTP_referer) 但剩下的你必须给自己 `UTM` 参数。 当您看到 `google adwords` 或 `email marketing` 这意味着 `UTM` 参数是从原始链接点击中记录的，然后存储在用户的Cookie中。 从此， [!DNL Google Analytics] 使用数据 [属性兴趣行为](../data-analyst/analysis/google-track-user-acq.md) 在您的网站上。 了解这些参数的用途有助于您了解如何最好地设置和使用UTM标记。

## UTM标记的最佳实践

下面列出了在使用 `UTM` 标记。

### 1.旨在标记您可以控制访问您网站的每个URL

每次您要求用户单击链接时，您都应设置 `UTM` 标记。 这包括您的所有电子邮件链接（您的电子邮件服务提供商可能有自动标记您的URL的方法）、广告链接、新闻文章、博客帖子。

### 2.使用工具创建URL

`UTM` — 标记的URL可能很麻烦。 使用工具，而不是尝试长时间键入它们 [这样](https://support.google.com/analytics/answer/1033867?hl=en) 来帮你。 这可确保您考虑将所有合理的参数添加到URL，然后即可将URL复制并粘贴出来。 要管理社交链接，请使用诸如 [!DNL Hootsuite] 包括用于向所有链接添加自定义URL参数的选项。

### 3.确保参数值中区分大小写

请记住标记 `utm\_source=adwords` 是与 `utm\_source=Adwords`. 考虑让所有内容都变小一些。

### 4.将UTM参数值存储在数据库中

每次发生交易或事件时，您都需要评估营销活动的绩效。 为此，您可以从 [[!DNL Google Analytics] cookie到数据库](../data-analyst/analysis/google-track-user-acq.md).

### 5.考虑如何命名营销活动

为了跟踪营销工作在一段时间内的改善情况，您需要明智地使用命名惯例。 使其保持简单，并尽可能减少。 复杂的命名系统很难维护。

在数据库中捕获此数据后，您可以通过更复杂的分析(包括 [客户生命周期值](../data-analyst/analysis/ess-expected-ltv.md), [重复购买率](../data-analyst/analysis/repurchase-behavior.md)和 [平均订单值](../data-analyst/analysis/basic-analytics.md).
