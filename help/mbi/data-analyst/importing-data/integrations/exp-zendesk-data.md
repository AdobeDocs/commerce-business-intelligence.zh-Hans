---
title: 預期Zendesk資料
description: 瞭解您可以從Zendesk匯入Commerce Intelligence的主要資料表，包括有關Zendesk資料的其他檔案的連結。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 預期 [!DNL Zendesk] 資料

晚於 [您已連線 [!DNL Zendesk] 帳戶](../integrations/zendesk.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤相關資料欄位以供分析。

本主題會探索您可從其中匯入的主要資料表格 [!DNL Zendesk] 到 [!DNL Adobe Commerce Intelligence]，包括其他檔案的連結關於 [!DNL Zendesk] 資料。

| 表格名稱 | 說明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 此 `Audits` 表格會記錄與票證相關的活動，包括狀態變更以及客戶和代理商回應。 此表格含有一個票證ID，可連結回 `Tickets` 表格，可讓您分析每個票證的首次回應時間和解決時間。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 此 `audit_~\_events` 表格是 `audits` 表格並記錄票證事件的其他詳細資料。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 此 `Organizations` 表格會記錄有關您一般使用者的公司資訊，例如名稱、ID、關聯的網域名稱、標籤及任何自訂欄位。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 此 `Tickets` 表格會記錄所有票證詳細資料，包括 `created_at` 時間戳記和 `requester\_id` 和 `assignee\_id`，可讓您將票證連結至中的一般使用者和代理 `Users` 表格。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 此 `ticket fields` 表格包含有關帳戶中基本文字欄位和自訂票證欄位的資訊。 此表格的屬性包含欄位 `ID`， `URL`， `type`， `title`， `description`， `position`， `requirement setting`、代理程式和一般使用者特定資訊，以及建立和更新資訊。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 此 `Users` 表格包含一般使用者和代理人的所有詳細資訊，包括個人姓名和電子郵件。 這可讓您分析一般使用者的參與度和代理程式的效能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 群組是代理程式在您的Zendesk帳戶中的組織方式。 此 `Groups` 表格記錄資訊，例如 `group ID`， `URL`， `name`以及建立和更新資訊。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 巨集是由您定義的動作，可修改票證欄位的值。 此表格包含巨集的標題、ID、動作、限制，以及建立和更新資訊等屬性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 此 `Tags` 表格包含您帳戶中所有標籤的清單。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表格包含票證量度的相關資料。 欄位包括 `ticket ID`， `URL`，以及群組、受指派人、重新開啟、回覆、回覆時間（以分鐘為單位）、完整解決時間和上次更新（例如狀態、受指派人或請求者）等資訊的數量。 |

{style="table-layout:auto"}

## 相關

* [正在連線Zendesk](../integrations/zendesk.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
