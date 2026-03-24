---
title: 预期Mixpanel数据
description: 浏览可从Mixpanel导入到 [!DNL Commerce Intelligence] 帐户中的主数据表。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# 预期[!DNL Mixpanel]数据

在连接[您的 [!DNL Mixpanel] 帐户](../integrations/mixpanel.md)后，您可以使用[Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)轻松跟踪相关数据字段以供分析。

本主题探讨可从[!DNL Mixpanel]导入到[!DNL Commerce Intelligence]帐户的主要数据表。 连接[!DNL Mixpanel]后将在Data Warehouse中创建以下表。 要查看所有可用于跟踪的字段，请单击表名列中的链接。

>[!NOTE]
>
>由于[!DNL Mixpanel] API的限制，不会复制历史数据(从连接到[!DNL Commerce Intelligence]日期起七(7)天之前的数据)。

| **表名** | **描述** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表包含原始事件数据，包括事件、事件日期和平台存储段。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表包含有关您的漏斗的数据，包括funnel ID、funnel时长（用户必须完成funnel的天数）以及funnel的开始和结束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 其中包含来自People Analytics的数据，包括会话ID、页面和用户信息以及上次查看用户的日期/时间。 |

{style="table-layout:auto"}

## 相关文档

* [正在连接 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
