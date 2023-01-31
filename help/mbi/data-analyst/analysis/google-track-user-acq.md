---
title: Google Analytics — 跟踪用户客户获取源数据概述
description: 了解如何按用户获取源对数据进行分段。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 按用户获取源划分区段

>[!NOTE]
>
>以下过程不支持 [!DNL GoogleUniversal Analytics].

能够按用户获取来源对数据进行分段对于有效管理营销计划至关重要。 了解新用户的客户获取来源可显示哪些渠道可获得最高的回报，并让您的团队能够满怀信心地分配营销资金。

如果您尚未跟踪数据库中的用户获取源， [!DNL MBI] 可以帮助您入门：

## 跟踪用户获取源

我们建议使用两种方法根据您的设置跟踪反向链接源数据：

### （选项1）通过 [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您利用 [!DNL Google Analytics E-Commerce] 为了跟踪您的订单和销售数据，您可以利用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 同步每个订单的引荐源数据。 这将允许您按引荐来源对收入和订单进行细分(例如， `utm_source` 或 `utm_medium`)，并通过 [!DNL MBI] 自定义维度，例如 `User's first order source`.

>[!NOTE]
>
>对于Shopify用户**:打开 [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) 在连接 [!DNL Google Analytics E-Commerce] 帐户 [!DNL MBI].

### （选项2）保存 [!DNL Google Analytics]数据库中的客户获取源数据

在本文中，我们将介绍如何保存 [!DNL Google Analytics] 将客户获取渠道信息放入您自己的数据库中 — 即 `source`, `medium`, `term`, `content`, `campaign`和 `gclid` 用户首次访问您的网站时存在的参数。 有关这些参数的说明，请参阅 [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). 然后，我们将探索一些功能强大的营销分析，这些分析可在 [!DNL MBI].

#### 为什么？

如果您只查看默认 [!DNL Google Analytics] 转化和客户获取量度，则无法获得整体信息。 虽然查看自然搜索与付费搜索的转化次数很有意思，但您可以使用该信息做什么？ 你应该花更多的钱搜索吗？ 这取决于来自该渠道的客户的价值，而这不是Google Analytics提供的。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 通过在 [!DNL Google Analytics]，但是此解决方案不适用于非电子商务网站，并且某些工具（如同类群组分析）在 [!DNL Google Analytics] 界面。

如果您希望向通过特定电子邮件促销活动获得的所有客户发送后续交易电子邮件，该怎么办？ 还是将客户获取数据与您的CRM系统相集成？ 在 [!DNL Google Analytics]  — 事实上，本公司违反服务条款 [!DNL Google Analytics] 用于存储标识个人的任何数据。  但这并不意味着您不能自己存储此数据。

#### 方法

[!DNL Google Analytics] 在名为 `__utmz`. 设置此Cookie后(由 [!DNL Google Analytics] 跟踪代码)，其内容将随该用户随后向您的域发起的每个请求一起发送。 例如，在PHP中，您可以查看 `$_COOKIE['__utmz']` 您会看到一个类似于以下内容的字符串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

显然，有一些客户获取源数据已编码到字符串中，我们测试了以确认这是访客的最新客户获取源和关联的促销活动数据。 现在我们只需要知道如何提取数据。 幸运的是，Justin Cutroni先前已描述了此编码的工作方式，并共享了一些javascript代码以提取关键信息位。

我们把这个代码翻译成 [在github上托管的PHP库](https://github.com/RJMetrics/referral-grabber-php).   要使用库，请 `include` 引用 `ReferralGrabber.php` 然后调用

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返回的 `$data` 数组将是键值的映射 `source`, `medium`, `term`, `content`, `campaign`, `gclid` 和各自的值。

我们建议向数据库中添加一个名为(例如， `user_referral`，其中包含以下列： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每当用户注册时，请获取反向链接信息并将其存储到此表。

#### 如何使用此数据

现在，我们正在保存用户获取源，如何使用它？

假设我们使用的是SQL数据库，并且 `users` 表，其结构如下：

| ID | 电子邮件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有机 |
| 2 | jim@abc.com | 2012-01-24 | google | cp |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 反向链接 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有机 |
| ... | ... | ... | ... | ... |

首先，我们可以针对您的数据库运行以下查询，以计算来自每个反向链接渠道的用户数量：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

结果将如下所示：

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 反向链接 | 55 |
| 其他 | 16 |

这很有趣，但用途有限。 我们真正想知道的是这些数字随时间的增长率，每个收购来源产生的收入额， [同类群组分析](http://cohortanalysis.com/) 来自每个来源的用户数量，以及来自其中一个渠道的用户将来作为客户返回的可能性。 执行这些分析所需的查询非常复杂，这也是我们构建 [!DNL MBI]. 借助这些信息，我们可以确定最赚钱的收购渠道，并相应地将营销时间和资金集中到营销上。

### 相关

* **[跟踪数据库中的用户设备、浏览器和操作系统数据](https://support.magento.com/hc/en-us/articles/360016732911)**
* **[发现最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)**
* **[连接 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)**
* **[提高广告活动的ROI](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM归因工作？](../analysis/utm-attributes.md)**
