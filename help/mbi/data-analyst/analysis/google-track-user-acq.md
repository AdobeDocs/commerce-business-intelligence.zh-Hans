---
title: Google Analytics — 跟踪用户获取Source数据概述
description: 了解如何按用户获取源划分您的数据。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# 按用户获取源分段

>[!NOTE]
>
>以下进程不支持[!DNL Google Universal Analytics]。

按用户获取来源划分数据的能力是有效管理营销计划的关键。 了解新用户的客户获取来源可显示哪些渠道产生最高回报，并可让您的团队自信地分配营销资金。

如果您尚未在数据库中跟踪用户客户获取源，[!DNL Adobe Commerce Intelligence]可以帮助您开始：

## 跟踪用户客户获取来源

[!DNL Adobe]建议使用两种方法根据您的设置跟踪引用源数据：

### （选项1）通过[!DNL Google Analytics E-Commerce]跟踪订单引用源数据

如果您使用[!DNL Google Analytics E-Commerce]跟踪您的订单和销售数据，则可以使用[!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md)同步每个订单的转介源数据。 这允许您按反向链接来源（例如，`utm_source`或`utm_medium`）对收入和订单进行分段。 您还可以通过[!DNL Commerce Intelligence]自定义维度（如`User's first order source`）了解客户获取来源。

### （选项2）将[!DNL Google Analytics]的客户获取源数据保存在数据库中

本主题介绍如何将[!DNL Google Analytics]客户获取渠道信息保存到您自己的数据库中 — 即用户首次访问您的网站时显示的`source`、`medium`、`term`、`content`、`campaign`和`gclid`参数。 有关这些参数的说明，请参阅[[!DNL Google Analytics] 文档](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article)。 然后，您探索一些可在[!DNL Commerce Intelligence]中使用此信息执行的强大营销分析。

#### 为什么？

如果您只是查看默认的[!DNL Google Analytics]转化和客户获取量度，则不会全面了解情况。 虽然查看自然搜索与付费搜索的转化数量很有趣，但您可以如何处理这些信息？ 您应该花更多钱进行付费搜索吗？ 这取决于来自该渠道的客户的价值，而Google Analytics无法提供这些价值。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce)通过在[!DNL Google Analytics]中存储事务数据来缓解此问题，但此解决方案不适用于非电子商务网站。 此外，在[!DNL Google Analytics]界面中执行同类群组分析等某些工具并不容易。

如果您希望通过电子邮件将跟进交易发送给从特定电子邮件促销活动获得的所有客户，该怎么办？ 或将客户获取数据与您的CRM系统集成？ 这在[!DNL Google Analytics]中是不可能的 — 事实上，它违反了[!DNL Google Analytics]的服务条款，不能存储任何标识个人的数据。 但是，您可以自行存储这些数据。

#### 方法

[!DNL Google Analytics]将访客反向链接信息存储在名为`__utmz`的Cookie中。 在此Cookie（由[!DNL Google Analytics]跟踪代码设置）设置后，其内容将随每个后续请求一起从该用户发送到您的域。 因此，例如，在PHP中，您可以签出`$_COOKIE['__utmz']`的内容，并且您会看到类似于下面的字符串：

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

显然有一些客户获取源数据已编码到字符串中。 测试以确认这是访客的最新客户获取来源和相关联的活动数据。 现在您需要知道如何提取数据。

此代码已转换为github](https://github.com/RJMetrics/referral-grabber-php)上托管的[PHP库。 要使用库，`include`引用`ReferralGrabber.php`，然后调用

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返回的`$data`数组是键`source`、`medium`、`term`、`content`、`campaign`、`gclid`及其相应值的映射。

Adobe建议向数据库中添加一个名为的表，例如`user_referral`，其列如下： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`。 每当用户注册时，请获取反向链接信息并将其存储在此表中。

#### 如何使用此数据

现在您正在保存用户客户获取源，怎样才能使用它？

假设您正在使用SQL数据库并且有一个具有以下结构的`users`表：

| ID | 电子邮件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有机 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 反向链接 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有机 |
| ... | ... | ... | ... | ... |

首先，您可以通过对数据库运行以下查询来统计来自每个反向链接渠道的用户数：

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

结果如下所示：

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 反向链接 | 55 |
| 其他 | 16 |

这很有趣，但用途有限。 您真正希望了解的是：

* 这些数字在一段时间内的增长率
* 每个购置来源产生的收入金额
* 来自每个源的[同类群组分析](https://en.wikipedia.org/wiki/Cohort_analysis)用户
* 这些渠道之一的用户将来作为客户返回的概率

进行这些分析所需的查询很复杂。 利用这些信息，您可以确定利润率最高的收购渠道，并相应地集中营销时间和资金。

### 相关

* **[了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)**
* **[连接你的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)**
* **[提高广告促销活动的ROI](../analysis/roi-ad-camp.md)**
* **[如何进行 [!DNL Google Analytics] UTM归因？](../analysis/utm-attributes.md)**
