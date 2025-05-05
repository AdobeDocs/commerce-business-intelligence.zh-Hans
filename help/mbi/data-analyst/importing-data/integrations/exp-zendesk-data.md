---
title: 预期Zendesk数据
description: 了解可从Zendesk导入Commerce Intelligence的主要数据表，包括指向有关Zendesk数据的其他文档的链接。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 预期[!DNL Zendesk]数据

在连接[您的 [!DNL Zendesk] 帐户](../integrations/zendesk.md)后，您可以使用[Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)轻松跟踪相关数据字段以供分析。

本主题探索可从[!DNL Zendesk]导入到[!DNL Adobe Commerce Intelligence]的主要数据表，包括指向有关[!DNL Zendesk]数据的其他文档的链接。

| 表名 | 描述 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | `Audits`表记录与票证关联的活动，包括状态更改以及客户和代理响应。 此表包含链接回`Tickets`表的票证ID，该表允许您分析每个票证的首次响应时间和解析时间。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | `audit_~\_events`表是`audits`表的子级，并记录票证事件的其他详细信息。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | `Organizations`表记录有关您最终用户的公司信息，如名称、ID、关联的域名、标记和任何自定义字段。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | `Tickets`表记录所有票证详细信息，包括`created_at`时间戳以及`requester\_id`和`assignee\_id`，这允许您分别将票证链接到`Users`表中的最终用户和代理。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | `ticket fields`表包含有关帐户中的基本文本字段和自定义票证字段的信息。 此表的属性包括字段`ID`、`URL`、`type`、`title`、`description`、`position`、`requirement setting`、特定于代理和最终用户的信息以及创建和更新信息。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | `Users`表包含有关最终用户和代理的所有详细信息，包括个人姓名和电子邮件。 这使您能够分析最终用户的参与和代理的性能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 组是代理在您的Zendesk帐户中的组织方式。 `Groups`表记录信息，如`group ID`、`URL`、`name`以及创建和更新信息。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 宏是您定义的修改票证字段值的操作。 此表包含宏的标题、ID、操作、限制以及创建和更新信息等属性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | `Tags`表包含您帐户中所有标记的列表。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表包含有关票证量度的数据。 字段包括`ticket ID`、`URL`以及组数、任务接受者、重新打开、回复、回复时间（以分钟为单位）、完整解决时间和上次更新（例如，状态、任务接受者或请求者）信息。 |

{style="table-layout:auto"}

## 相关

* [正在连接Zendesk](../integrations/zendesk.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
