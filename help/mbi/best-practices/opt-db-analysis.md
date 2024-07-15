---
title: 优化数据库以进行分析
description: 了解如何优化数据库以供分析。
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# 优化数据库

为[!DNL Adobe Commerce Intelligence]使用操作数据库的主要好处是，无需构建或修改任何内容即可收集数据。 有价值的信息已经存在 — 您只需将其解锁。

本主题包含一些建议，可帮助您优化数据库以进行分析，并从原始数据中得出切实可行的见解。

## 不删除数据

>[!TIP]
>
>影响您的业务（以及您自己的服务条款）的本地和国际法规可能会影响您可以保留的数据类型以及保留多长时间。 遵守这些法律应该是您的首要任务。

当订单被取消、用户停用其帐户或产品被停产时，很想删除数据库中的相关信息。 增加表格数量并消除杂乱似乎是一个明智的想法。 但是，删除行意味着此信息将永远丢失，或者您需要仔细研究旧备份才能找到它。

相反，您可以向表中添加一个状态列，以指示该行何时不再处于活动状态或相关状态。 还建议添加一列来存储进行更改的日期，或创建历史更改日志。 如果表变得足够大，性能开始受到影响，请考虑将旧数据归档到用于分析的表中。

## 很少覆盖数据

应谨慎覆盖数据。

以登录日期为例，许多公司存储的是上次登录日期，而不是历史登录次数表。 虽然您可能只需要上次登录日期即可正常使用，但从Analytics的角度来看，被覆盖的数据会造成巨大损失。 如果不保留这些操作的完整日志，则无法查看有多少用户长时间离开然后再重新激活。 它还使得无法基于登录构建用户参与同类群组分析等内容。

通常，如果由于某种用户操作而更新记录，则不要覆盖有关上一个或单独用户操作的信息。

## 包括`Updated_at`列，用于随时间更新的数据

如果表的行将具有随时间变化的值，例如&#x200B;**order\_status**&#x200B;从`processing`更改为`complete`，则包含一个&#x200B;**updated\_at**&#x200B;列以记录最新更改的时间。 当&#x200B;**updated\_at**&#x200B;日期对应于&#x200B;**created\_at**&#x200B;日期时，请确保首次插入新数据行时有&#x200B;**updated\_at**&#x200B;值可用。

除了优化分析之外，**updated\_at**&#x200B;列还允许您使用[增量复制方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)，这有助于缩短更新周期的长度。

## 商店用户获取Source

最常见的错误之一是[用户获取源](../data-analyst/analysis/google-track-user-acq.md) (UAS)未存储在操作数据库中。 在出现问题的大多数情况下，仅通过[!DNL Google Analytics]或某些其他Web分析工具跟踪UAS。 虽然这些工具可能很有价值，但仅在这些工具中存储UAS存在一些缺点；例如，无法从这些工具中提取用户级数据。 如果可能的话，这通常是一个困难的过程。 获取此信息并将其与其他来源的数据（例如也存储在数据库中的行为和事务性信息）相匹配应该很容易。

将UAS存储在您自己的数据库中，通常是在线企业对其分析能力所能做的最大改进。 这允许UAS分析销售额、用户参与度、回收期、客户存留期值、流失率以及其他关键指标。 [在决定投资营销资源的位置时，此数据至关重要](../data-analyst/analysis/most-value-source-channel.md)。

太多公司只关注寻找以最低成本提供新用户的渠道。 如果您没有跟踪从每个渠道获得的用户的质量，则可能会吸引没有产生业务价值的用户。

## 数据表设置

### 设置主键

[主键](https://en.wikipedia.org/wiki/Unique_key)是未更改的列（或列集），它在表中生成唯一值。 主键非常重要，因为它们可确保在[!DNL Commerce Intelligence]中正确复制表。

构建主键时，为自动增量的列使用整数数据类型。 Adobe建议您尽可能避免使用多列主键。

如果您的表是SQL视图，请添加可充当主键的列。 [!DNL Commerce Intelligence]能够自动将此列标识为主键。

### 为数据列分配数据类型

如果数据列没有分配的[数据类型](https://en.wikipedia.org/wiki/Data_type)，则[!DNL Commerce Intelligence]猜测要使用哪种数据类型。 如果Adobe猜测不正确，则在System支持团队将列调整为正确的数据类型之前，您可能无法执行相关分析。 例如，如果日期列假定为数字数据类型，则可以使用日期维度显示一段时间的趋势。

### 如果您有多个数据库，请向数据表添加前缀

如果有多个数据库连接到[!DNL Commerce Intelligence]，Adobe建议向表添加前缀以避免混淆。 前缀可帮助您记住量度或数据维度的来源位置。
