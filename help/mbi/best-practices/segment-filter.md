---
title: 分段和过滤的建议数据维度
description: 了解分段和过滤的最佳实践。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# 分段和筛选

良好的细分将表面统计数据转变为推动决策的商务量度。

想知道您最有价值的客户是谁？ 您最有价值的营销渠道是什么？ 您的哪些产品移动得更快？为什么？ 要得到这些答案中的任何一个，您必须从对数据进行分段开始。

本主题介绍经常向客户推荐的关键区段。 此外，还详细介绍了这些区段可以帮助您回答的问题。 从技术上讲，区段是数据库中的数据列。 在[!DNL Adobe Commerce Intelligence]中，它们称为维度。

![显示关键客户区段和过滤器的仪表板](../../mbi/assets/mbi-critical-segments.png)


## 用户区段

用户区段可帮助您了解用户的身份及其行为方式。

* **年龄/出生年**：您的用户有多大？ 您最活跃的用户多大岁数？ 通常，将值分到多个范围中以进行更有效的分析很有意义。
* **性别**：不同的性别与您的网站互动方式是否不同？
* **地址**：您的用户来自何处？ 您应该将营销工作重点放在特定区域吗？ 您最近的广告活动是否在目标区域按预期执行？
* **客户获取来源**\：您知道用户来自哪个营销渠道吗？ 他们是点击广告还是通过搜索找到您？ [按用户客户获取源对您的数据进行分段](../data-analyst/analysis/google-track-user-acq.md)是优化新客户获取的第一步。 第二步是花更多钱在有效领域，扼杀无效领域。
* **注册设备**：用户是否通过移动设备应用程序或网站进行注册？ iOS还是Android™？ 您的移动用户群是否足够大，可以分配更多资源来开发您的移动产品？ 如果尚未跟踪此内容，请参阅此主题[关于跟踪用户设备](../data-analyst/analysis/track-usr-dev-browser.md)。
* **由**&#x200B;推荐：谁是您最有影响力的人？ 有多少用户被其他人直接引用？
* **行业**：如果您是B2B企业，您的用户从事哪些行业？ 哪些贸易组织值得加入？
* **调查回复**：如果您执行客户调查，请将回复用作区段，以便进行更深入的分析。 您可以提出一些问题，以补充您已经知道的有关用户的信息，或确认您的猜测。
* **第一订单金额和产品类别**：用户的第一订单与未来购买模式之间是否存在关联？

## 订单/事件区段

订单和事件区段有助于分析一段时间内的用户行为和参与度。

* **[!UICONTROL Billing / Shipping Address]**：您的大多数订单来自何处？ 账单地址和运送地址之间是否有区别？
* **[!UICONTROL Status]**：有多少订单未能完成？ 过去7天未完成订单的比率是多少？
* **[!UICONTROL Customer acquisition source]**：除了在用户级别跟踪用户获取数据之外，您还可以在订单或事件级别[跟踪该数据](../data-analyst/analysis/google-track-user-acq.md)。 通过某个源注册的用户很可能会继续通过其他源访问您的网站。
* **[!UICONTROL Device]**：移动订单的数量是否正在增加？ 您的收入中有多少是通过移动购买产生的？ (如果尚未跟踪此项，请参阅此主题[关于跟踪订单设备数据](../data-analyst/analysis/track-usr-dev-browser.md)。
* **[!UICONTROL Fulfillment Center]**：您的哪个履行中心产生的收入最多？ 如果您正在分析订单时间和发运时间之间的差异，那么哪个履行中心的响应最快？
* **[!UICONTROL Delivery Carrier]**：哪家是最受欢迎的运营商？ 哪个运营商的退货数量最少？
* **[!UICONTROL Discount / Coupon Codes]**：您的促销活动是否确实产生了额外的业务？ 除了待售的商品外，您的客户还购买了多少其他商品？ 优惠券如何影响您的平均订单价值？ 折扣产品与非折扣产品的平均利润率是多少？
* **[!UICONTROL Satisfaction / Rating]**：您的客户对其订单的满意度如何？ 您的客户是否可能会向您推荐业务？

## 产品区段

产品区段可帮助您制定促销决策。

* **[!UICONTROL Merchant / Brand]**：某个特定品牌的销售速度是否比其他品牌快？ 哪些品牌表现不佳？
* **[!UICONTROL Type / Category]**：不同的用户区段是否喜欢不同类型的产品？ 哪些产品类别产生的重复业务最多？
* **[!UICONTROL Discount / Coupon Codes]**：促销活动是否会影响非折扣产品的销售？ 优惠券如何影响产品的感知价值？
* **[!UICONTROL Social Activity]**：在社交媒体上产生的轰动与产品的销售量之间是否存在关联？
* **[!UICONTROL Size / Variant]**：您需要每个变体的库存比率是多少？ 哪些变体可以按折扣率出售？

如果您对销售感兴趣，请查看[如何使用产品区段推动重复业务](../data-analyst/analysis/most-value-source-channel.md)。

## 建立客户配置文件

分段专家可能希望超越一维切片，开始建立真正的客户档案。 例如，13岁至24岁通过移动设备注册的人被归入“Young &amp; Mobile”组。 该组的行为与您用户群的其余成员相比如何？

这种分析是财富1000强公司的营销人员整天都在做的事情。 在诸如[!DNL Commerce Intelligence]之类的基于云的业务智能平台出现之前，我们其他人基本上无法看到它。 幸运的是，现在情况已发生了变化。

## 跟踪新区段

按上述维度划分量度的第一步是确保跟踪数据库中的此数据。 如果未跟踪此数据，请与您的技术团队会面，并找到开始跟踪此数据的方法。

确认在数据库中跟踪数据后，[联系支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以将维度推送到[!DNL Commerce Intelligence]量度和图表。 您还可以使用&#x200B;*字段管理*&#x200B;工具在[!DNL Commerce Intelligence]中跟踪这些字段。

## 相关

* [优化数据库以进行分析](../best-practices/opt-db-analysis.md)
