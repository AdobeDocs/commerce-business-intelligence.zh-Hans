---
title: 分段和过滤的建议数据Dimension
description: 了解分段和筛选的最佳实践。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# 分段和筛选

良好的细分是将肤浅的统计数据转变为推动决策的商业量度。

想知道您最有价值的客户是谁？ 您最有价值的营销渠道是什么？ 您的哪些产品移动得更快？为什么？ 要得到这些答案中的任何一个，您必须从对数据进行分段开始。

本主题涵盖通常向客户推荐的关键区段。 此外，还详细介绍了这些区段可以帮助您回答的问题。 从技术上讲，区段是数据库中的数据列。 In [!DNL Adobe Commerce Intelligence]，则这些维度称为维度。

![](../../mbi/assets/mbi-critical-segments.png)


## 用户区段

用户区段可帮助您了解用户的身份及其行为。

* **年龄/出生年份**：您的用户的年龄是多少？ 您最活跃的用户多大岁数？ 通常，有必要将这些值划分到不同的范围中，以便进行更有效的分析。
* **性别**：不同的性别与您的网站的互动方式是否不同？
* **地址**：您的用户来自何处？ 您应该将营销工作重点放在特定区域吗？ 您最近的广告营销活动是否在目标区域按预期执行？
* **客户获取来源**\：您知道用户来自哪个营销渠道吗？ 他们点击了广告还是通过搜索找到了您？ [按用户获取来源划分您的数据段](../data-analyst/analysis/google-track-user-acq.md) 是优化新客户获取的第一步。 第二步是在有效领域投入更多资金，扼杀无效领域。
* **注册装置**：用户是通过您的移动应用程序还是网站注册的？ iOS还是Android™？ 您的移动用户基础是否足够大，可以分配更多资源来开发您的移动产品？ 如果您尚未跟踪此内容，请参阅此主题 [关于跟踪用户设备](../data-analyst/analysis/track-usr-dev-browser.md).
* **引用者**：谁是您最有影响力的人？ 有多少用户被其他人直接引用？
* **行业**：如果您是一家B2B企业，您的用户从事哪些行业？ 哪些贸易组织值得加入？
* **调查回复**：如果您执行客户调查，请将响应作为区段使用，以实现更深入的分析。 您可以提出一些问题，以补充您已经知道的有关用户的信息，或确认您的猜测。
* **第一订单金额和产品类别**：用户的首次订购与未来购买模式之间是否存在相关性？

## 订单/事件区段

订单和事件区段有助于分析一段时间内的用户行为和参与度。

* **[!UICONTROL Billing / Shipping Address]**：您的大多数订单来自哪里？ 帐单地址与送货地址之间是否有区别？
* **[!UICONTROL Status]**：您有多少订单未能完成？ 过去7天未完成订单的比率是多少？
* **[!UICONTROL Customer acquisition source]**：除了在用户级别跟踪用户获取数据之外，您还可以 [在订单或事件级别跟踪它](../data-analyst/analysis/google-track-user-acq.md). 通过某个源注册的用户很可能会继续通过其他源访问您的网站。
* **[!UICONTROL Device]**：移动订单数量是否有所增加？ 您的收入中有多少是通过移动购买产生的？ (如果您尚未跟踪此内容，请参阅此主题 [关于跟踪订单设备数据](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**：您的哪个履行中心产生的收入最多？ 如果您正在分析订单时间与发运时间之间的差异，则哪个履行中心的响应速度最快？
* **[!UICONTROL Delivery Carrier]**：哪一家是最受欢迎的运营商？ 哪个运营商的退货数量最少？
* **[!UICONTROL Discount / Coupon Codes]**：您的促销活动是否确实带来了额外的业务？ 除了待售的商品外，您的客户还购买了多少其他商品？ 优惠券如何影响您的平均订单价值？ 折扣产品与非折扣产品的平均利润是多少？
* **[!UICONTROL Satisfaction / Rating]**：客户对订单的满意度如何？ 您的客户是否可能向您推荐业务？

## 产品区段

产品区段可帮助您制定促销决策。

* **[!UICONTROL Merchant / Brand]**：某个特定品牌的销售速度是否比其他品牌快？ 哪些品牌表现不佳？
* **[!UICONTROL Type / Category]**：不同的用户区段喜欢不同类型的产品吗？ 哪些产品类别产生的重复业务最多？
* **[!UICONTROL Discount / Coupon Codes]**：促销活动是否会影响非折扣产品的销售？ 优惠券如何影响您产品的感知价值？
* **[!UICONTROL Social Activity]**：社交媒体上产生的轰动与产品的销量之间是否有相关性？
* **[!UICONTROL Size / Variant]**：您需要每个变体的库存比率是多少？ 哪些变体可以按折扣率出售？

如果您对商品销售感兴趣，请查看 [如何使用产品区段推动业务重复](../data-analyst/analysis/most-value-source-channel.md).

## 建立客户配置文件

分段专家可能希望超越一维切片，开始建立真正的客户档案。 例如，13岁至24岁通过移动设备注册的人被放入“Young &amp; Mobile”组。 该组的行为与您用户群的其余部分有何不同？

这种分析是《财富》1000强企业的营销人员每天都在做的事情。 在诸如以下基于云的业务智能平台问世之前 [!DNL Commerce Intelligence]我们其余人基本上都买不起。 幸运的是，现在情况已经发生了变化。

## 跟踪新区段

按上述维度划分量度的第一步是确保跟踪数据库中的此数据。 如果未跟踪此数据，请与您的技术团队会面，并找到开始跟踪此数据的方法。

确认在数据库中跟踪数据后， [联系支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 将维度推送到 [!DNL Commerce Intelligence] 量度和图表。 您还可以使用 *字段管理* 用于跟踪这些字段的工具 [!DNL Commerce Intelligence].

## 相关

* [优化数据库以进行分析](../best-practices/opt-db-analysis.md)
