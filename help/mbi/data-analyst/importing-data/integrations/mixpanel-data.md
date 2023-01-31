---
title: 预期的Mixpanel数据
description: 浏览可从Mixpanel导入到 [!DNL MBI] 帐户。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# 预期 [!DNL Mixpanel] 数据

之后 [您已连接 [!DNL Mixpanel] 帐户](../integrations/mixpanel.md)，则可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。

在本文中，我们将探索可从中导入的主要数据表 [!DNL Mixpanel] 到 [!DNL MBI] 帐户。 连接Mixpanel后，将在data warehouse中创建下表。 要查看所有可用于跟踪的字段，请单击表名称列中的链接。

>[!NOTE]
>
>由于 [!DNL Mixpanel] API，历史数据 — 连接日期后七(7)天内的数据 [!DNL MBI]  — 不会复制。

| **表名称** | **描述** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | 此表包含原始事件数据，包括事件、事件日期和平台存储段。 |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | 此表包含有关漏斗的数据，包括漏斗ID、漏斗长度（用户必须完成漏斗的天数#）以及漏斗的开始和结束日期。 |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | 其中包含来自People Analytics的数据，包括会话ID、页面和用户信息，以及用户上次被看到的日期/时间。 |

{style=&quot;table-layout:auto&quot;}

## 相关文档

* [连接 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
