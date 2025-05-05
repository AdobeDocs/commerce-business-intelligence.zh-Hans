---
title: 预期Stripe数据
description: 探索可从Stripe导入Commerce Intelligence的主要数据表。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 预期[!DNL Stripe]数据

在连接[您的 [!DNL Stripe] 帐户](../integrations/stripe.md)后，您可以使用[Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)轻松跟踪相关数据字段以供分析。

本主题探讨可从[!DNL Stripe]导入到[!DNL Commerce Intelligence]中的主要数据表。 安装完成后，将在Data Warehouse中创建以下表。 单击“表名”列中的链接可了解有关每个表中属性的更多信息。

| **表名** | **描述** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 客户对象允许您执行经常性费用并跟踪与同一客户关联的多项费用。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 此表包含有关信用卡和借记卡费用的信息，包括金额、币种、状态、客户ID等。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 此表包含有关要向客户应用的折扣百分比或折扣金额的信息。 优惠券只适用于发票，不适用于一次性费用。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 此表包含有关发票的信息，包括缺款金额、订阅、发票项目、任何自动按比例分配调整等。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 此表包含您网站上不同产品和功能级别的定价信息。 例如，您可能的基本功能计划为每月10美元，而高级功能计划为每月20美元。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 此表包含您的客户所属的订阅计划的详细信息。 属性包括客户ID、状态、已取消/已于日期结束、税费百分比、试用信息等。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 通过事件，您可以了解某个帐户中发生的有趣事件。 [发生有趣的事件时](https://stripe.com/docs/api/events/types)，将创建一个新的事件对象。 例如，当费用在`charge.succeeded`事件之后创建时；或当无法支付发票时，创建`invoice.payment\_failed`事件。 |

{style="table-layout:auto"}

>[!NOTE]
>
>许多API请求都可能会导致创建多个事件。 例如，如果您为客户创建订阅，您将同时收到`customer.subscription.created`事件和`charge.succeeded`事件。

## 相关：

* [正在连接 [!DNL Stripe]](../integrations/stripe.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
