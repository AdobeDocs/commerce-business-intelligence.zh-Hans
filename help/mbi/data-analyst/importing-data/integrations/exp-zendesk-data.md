---
title: 预期的Zendesk数据
description: 了解可从Zendesk导入MBI的主要数据表，包括指向有关Zendesk数据的其他文档的链接。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# 预期的Zendesk数据

之后 [您已连接 [!DNL Zendesk] 帐户](../integrations/zendesk.md)，则可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。

在本文中，我们将探索可从中导入的主要数据表 [!DNL Zendesk] into [!DNL MBI]，包括指向其他文档的链接，关于 [!DNL Zendesk] 数据。

| 表名称 | 描述 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 的 `Audits` 表记录与票证关联的活动，包括状态更改以及客户和代理响应。 此表包含一个票证ID，该票证ID可链接回 `Tickets` 表格，用于分析每个票证的首次响应时间和解决时间。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 的 `audit_~\_events` 表是 `audits` 表格和记录票证事件的其他详细信息。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 的 `Organizations` 表记录有关最终用户的公司信息，如名称、ID、关联的域名、标记和任何自定义字段。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 的 `Tickets` 表记录所有票证详细信息，包括 `created_at` 时间戳以及 `requester\_id` 和 `assignee\_id`，用于将票证链接到 `Users` 表。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 的 `ticket fields` 表包含有关帐户中基本文本字段和自定义票证字段的信息。 此表的属性包括字段 `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`、代理和最终用户特定信息，以及创建和更新信息。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 的 `Users` 该表包含有关最终用户和代理的所有详细信息，包括个人姓名和电子邮件。 这样，您就可以分析最终用户的参与度以及代理的性能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 组是在Zendesk帐户中组织座席的方式。 的 `Groups` 表记录信息，如 `group ID`, `URL`, `name`、以及创建和更新信息。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 宏是您定义的用于修改票证字段值的操作。 此表包含宏的标题、ID、操作、限制以及创建和更新信息等属性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 的 `Tags` 表包含您帐户中所有标记的列表。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表包含有关票证量度的数据。 字段包括 `ticket ID`, `URL`、组数、受让人、重新打开数、回复数、回复时间（以分钟为单位）、完整解决时间和上次更新（例如，状态、受让人或请求者）信息。 |

{style=&quot;table-layout:auto&quot;}

## 相关

* [连接Zendesk](../integrations/zendesk.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
