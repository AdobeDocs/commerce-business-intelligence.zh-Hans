---
title: 预期Zendesk数据
description: 了解您可以从Zendesk导入Commerce Intelligence的主要数据表，包括指向有关Zendesk数据的其他文档的链接。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 预期 [!DNL Zendesk] 数据

晚于 [您已连接 [!DNL Zendesk] 帐户](../integrations/zendesk.md)，您可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段以供分析。

本主题介绍可从其中导入的主要数据表 [!DNL Zendesk] 到 [!DNL Adobe Commerce Intelligence]，包括指向以下内容的其他文档的链接： [!DNL Zendesk] 数据。

| 表名 | 描述 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 此 `Audits` 表记录与票证相关的活动，包括状态更改以及客户和座席回应。 此表包含一个票证ID，该票证将链接回 `Tickets` 表，用于分析每个票证的首次响应时间和解决时间。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 此 `audit_~\_events` table是 `audits` 表格并记录票证事件的其他详细信息。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 此 `Organizations` 表记录有关最终用户的公司信息，如名称、ID、关联的域名、标记和任何自定义字段。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 此 `Tickets` 表记录所有票证详细信息，包括 `created_at` 时间戳和 `requester\_id` 和 `assignee\_id`，以便将票证链接到中的最终用户和代理 `Users` 表。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 此 `ticket fields` 该表包含有关帐户中的基本文本字段和自定义票证字段的信息。 此表的属性包括字段 `ID`， `URL`， `type`， `title`， `description`， `position`， `requirement setting`、代理和最终用户特定信息以及创建和更新信息。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 此 `Users` 该表包含有关最终用户和代理的所有详细信息，包括个人姓名和电子邮件。 这允许您分析最终用户的参与和代理的性能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 组是代理在您的Zendesk帐户中的组织方式。 此 `Groups` 表记录信息，例如 `group ID`， `URL`， `name`以及创建和更新信息。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 宏是由您定义的修改票证字段值的操作。 此表包含宏的标题、ID、操作、限制以及创建和更新信息等属性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 此 `Tags` 表格包含您帐户中所有标记的列表。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表包含有关票证量度的数据。 字段包括 `ticket ID`， `URL`，以及组、被分派人、重新打开、回复、回复时间（以分钟为单位）、完整解决时间和上次更新（例如，状态、被分派人或申请人）信息的数量。 |

{style="table-layout:auto"}

## 相关

* [正在连接Zendesk](../integrations/zendesk.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
