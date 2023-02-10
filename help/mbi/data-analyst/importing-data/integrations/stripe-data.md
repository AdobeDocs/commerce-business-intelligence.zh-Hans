---
title: 预期条带数据
description: 浏览可从条带导入到 [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 预期 [!DNL Stripe] 数据

之后 [您已连接 [!DNL Stripe] 帐户](../integrations/stripe.md)，则可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。

在本文中，我们将探索可从中导入的主要数据表 [!DNL Stripe] into [!DNL MBI]. 完成设置后，将在您的data warehouse中创建以下表。 单击“表名称”列中的链接可了解有关每个表属性的更多信息。

| **表名称** | **描述** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 客户对象允许您执行经常性费用并跟踪与同一客户关联的多个费用。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 此表包含有关信用卡和借记卡费用的信息，包括金额、货币、状态、客户ID等。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 此表包含有关您可能希望向客户申请的折扣百分比或折扣金额的信息。 请注意，优惠券仅适用于发票；他们不适用于一次性收费。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 此表包含有关发票的信息，包括欠款、订阅、发票项、任何自动按比例分配调整等。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 此表包含网站上不同产品和功能级别的定价信息。 例如，您可能拥有基本功能的月费计划为10美元，高级功能的月费计划为20美元。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 此表包含客户所属订阅计划的详细信息。 属性包括客户ID、状态、取消/结束日期、税百分比、试用信息等。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 事件让您了解刚刚在帐户中发生的一些有趣的事情。 [当发生有趣事件时](https://stripe.com/docs/api/events/types)，则会创建新事件对象。 例如，当充电成功时 `charge.succeeded` 事件；或，当发票无法支付时 `invoice.payment\_failed` 事件。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>许多API请求可能会导致创建多个事件。 例如，如果您为客户创建新订阅，您将同时收到 `customer.subscription.created` 事件和  `charge.succeeded` 事件。

## 相关：

* [连接 [!DNL Stripe]](../integrations/stripe.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
