---
title: 預期的資料條資料
description: 探索可從Stripe匯入Commerce Intelligence的主要資料表。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 預期 [!DNL Stripe] 資料

晚於 [您已連線 [!DNL Stripe] 帳戶](../integrations/stripe.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤相關資料欄位以供分析。

本主題會探索您可從其中匯入的主要資料表格 [!DNL Stripe] 到 [!DNL Commerce Intelligence]. 安裝完成後，會在您的Data Warehouse中建立下清單格。 按一下「表格名稱」資料欄中的連結，以進一步瞭解每個表格中的屬性。

| **表格名稱** | **說明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 客戶物件可讓您執行重複產生費用，並追蹤與同一客戶相關聯的多重費用。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 此表格包含信用卡與借記卡費用的相關資訊，包括金額、幣別、狀態、客戶識別碼等。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 此表格包含您可能想要套用至客戶的折扣百分比或折扣金額的相關資訊。 優惠券只適用於商業發票，不適用於一次性費用。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 此表格包含有關商業發票的資訊，包括缺款金額、訂閱、商業發票專案、任何自動攤派調整等等。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 此表格包含您網站上不同產品和功能層級的定價資訊。 例如，您可能對基本功能有$10美元/月的計畫，而高級功能有$20美元/月的計畫。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 此表格包含您客戶所屬的訂閱計畫的詳細資料。 屬性包括客戶ID、狀態、已取消/結束日期、稅捐百分比、試用資訊等。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 事件可讓您瞭解帳戶中發生的有趣事件。 [發生有趣事件時](https://stripe.com/docs/api/events/types)，則會建立新的事件物件。 例如，當充電成功時 `charge.succeeded` 事件已建立；或當商業發票無法支付時 `invoice.payment\_failed` 事件已建立。 |

{style="table-layout:auto"}

>[!NOTE]
>
>許多API請求都可能導致建立多個事件。 例如，如果您為客戶建立訂閱，您會同時收到 `customer.subscription.created` 事件和  `charge.succeeded` 事件。

## 相關：

* [正在連線 [!DNL Stripe]](../integrations/stripe.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
