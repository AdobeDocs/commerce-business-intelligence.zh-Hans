---
title: Google Analytics — 跟踪用户获取源数据概述
description: 了解如何按用户获取源划分您的数据。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# 按用户获取来源分段

>[!NOTE]
>
>以下流程不支持 [!DNL Google Universal Analytics].

按用户获取来源划分数据的能力是有效管理营销计划的关键。 了解新用户的客户获取来源可显示哪些渠道产生最高回报，并可让您的团队自信地分配营销资金。

如果您尚未在数据库中跟踪用户客户获取源， [!DNL Adobe Commerce Intelligence] 可以帮助您入门：

## 跟踪用户获取源

[!DNL Adobe] 建议使用两种方法根据您的设置跟踪反向链接源数据：

### （选项1）通过以下方式跟踪订单反向链接源数据： [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您使用 [!DNL Google Analytics E-Commerce] 要跟踪您的订单和销售数据，您可以使用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 以同步每个订单的反向链接源数据。 这允许您按反向链接来源对收入和订单进行分段(例如， `utm_source` 或 `utm_medium`)。 您还可以通过以下方式了解客户获取来源 [!DNL Commerce Intelligence] 自定义维度，例如 `User's first order source`.

>[!NOTE]
>
>**对于Shopify用户**：打开 [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) 在连接您的 [!DNL Google Analytics E-Commerce] 目标帐户 [!DNL Commerce Intelligence].

### （选项2）保存 [!DNL Google Analytics]&#39;数据库中的客户获取源数据

本主题介绍如何保存 [!DNL Google Analytics] 客户获取渠道信息放入您自己的数据库 —  `source`， `medium`， `term`， `content`， `campaign`、和 `gclid` 用户在首次访问您的网站时存在的参数。 有关这些参数的说明，请查看 [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 然后，您会探索可以使用此信息在中执行的一些强大的营销分析 [!DNL Commerce Intelligence].

#### 为什么？

如果您只是查看默认 [!DNL Google Analytics] 转化和客户获取量度，您可能无法全面了解相关信息。 虽然查看自然搜索与付费搜索的转化次数很有趣，但您可以如何处理这些信息？ 您应该花更多钱进行付费搜索吗？ 这取决于来自该渠道的客户的价值，而这不是Google Analytics提供的东西。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 通过将事务数据存储到来缓解此问题 [!DNL Google Analytics]，但此解决方案不适用于非电子商务网站。 此外，同类群组分析等特定工具在中不易操作 [!DNL Google Analytics] 界面。

如果您希望通过电子邮件将跟进交易发送给从特定电子邮件促销活动获得的所有客户，该怎么办？ 或将客户获取数据与您的CRM系统集成？ 这是不可能的 [!DNL Google Analytics]  — 事实上，这违反了 [!DNL Google Analytics] 存储任何可标识个人的数据。 但是，您可以自行存储这些数据。

#### 方法

[!DNL Google Analytics] 将访客反向链接信息存储在名为的Cookie中 `__utmz`. 设置此Cookie后(由 [!DNL Google Analytics] 跟踪代码)，则其内容将随来自该用户的每个后续请求一起发送到您的域。 因此，例如，在PHP中，您可以检出 `$_COOKIE['__utmz']` 你会看到一个类似这样的字符串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

显然有一些客户获取源数据已编码到字符串中。 对此进行测试，以确认这是访客的最新客户获取源和相关联的促销活动数据。 现在您需要知道如何提取数据。

此代码已转换为 [在github上托管的PHP库](https://github.com/RJMetrics/referral-grabber-php). 要使用库， `include` 引用 `ReferralGrabber.php` 然后调用

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返回的 `$data` 数组是键的映射 `source`， `medium`， `term`， `content`， `campaign`， `gclid`，以及它们各自的值。

[!DNL Adobe] 建议向数据库中添加一个名为的表，例如 `user_referral`，具有以下列： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每当用户注册时，请获取反向链接信息并将其存储到此表中。

#### 如何使用此数据

现在您正在保存用户客户获取源，如何使用该源？

假设您正在使用SQL数据库并且具有 `users` 表格的下列结构：

| ID | 电子邮件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有机 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 反向链接 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有机 |
| ... | ... | ... | ... | ... |

首先，您可以通过对数据库运行以下查询来计数来自每个反向链接渠道的用户数：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

结果如下所示：

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 反向链接 | 55 |
| 其他 | 16 |

这很有趣，但用途有限。 您真正想了解的是：

* 这些数字在一段时间内的增长率
* 每个购置来源产生的收入金额
* a [同类群组分析](https://en.wikipedia.org/wiki/Cohort_analysis) 来自每个源的用户的数量
* 这些渠道之一的用户将来返回为客户的可能性。

执行这些分析所需的查询很复杂。 利用这些信息，您可以确定利润率最高的收购渠道，并相应地集中营销时间和资金。

### 相关

* **[了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)**
* **[连接您的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)**
* **[提高广告促销活动的ROI](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM归因工作？](../analysis/utm-attributes.md)**
