---
title: 预期Mixpanel数据
description: 探索可从Mixpanel导入的主要数据表 [!DNL Commerce Intelligence] 帐户。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 预期 [!DNL Mixpanel] 数据

之后 [您已将 [!DNL Mixpanel] 帐户](../integrations/mixpanel.md)，您可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段以供分析。

本主题探讨可从其中导入的主要数据表 [!DNL Mixpanel] 到您的 [!DNL Commerce Intelligence] 帐户。 连接后将在Data Warehouse中创建以下表 [!DNL Mixpanel]. 要查看所有可用于跟踪的字段，请单击表名列中的链接。

>[!NOTE]
>
>由于 [!DNL Mixpanel] API、历史数据 — 从连接日期起七(7)天以前的数据 [!DNL Commerce Intelligence]  — 未复制。

| **表名称** | **描述** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表包含原始事件数据，包括事件、事件日期和平台存储段。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表包含有关漏斗的数据，包括漏斗ID、漏斗长度（用户必须完成漏斗的天数）以及漏斗的开始和结束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 其中包含来自People Analytics的数据，包括会话ID、页面和用户信息以及上次查看用户的日期/时间。 |

{style="table-layout:auto"}

## 相关文档

* [正在连接 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
