---
title: 预期[!DNL Google ECommerce]数据
description: 了解与Google电子商务共享的数据类型。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 预期[!DNL Google ECommerce] 数据

在 [!DNL Google ECommerce] 帐户已成功连接到 [!DNL MBI]，则系统将开始将数据导入名为的表 `ecommerce`. 此表将记录每个交易的数据行。 这包括以下顺序级别的数据列：

| 列名称 | 描述 |
|-----|-----|
| `\_id` | 此列是主键。 |
| `accountId` | 此列包含与您的 [!DNL Google Analytics] 电子商务帐户。 |
| `profileName` | 此列包含 [!DNL Google Analytics] 配置文件名称。 |
| `profileId` | 此列包含 [!DNL Google Analytics] 配置文件ID。 |
| `socialNetwork` | 此列包含社交网络的名称(例如， [!DNL Facebook]或 [!DNL YouTube]) |
| `campaign` | 此列包含促销活动名称(例如， [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en))。 |
| `medium` | 此列包含媒体名称(例如， [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | 此列包含源名称。 (例如， [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | 此列包含关键词描述(例如， [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | 此列包含订单ID。 这将用于将反向链接数据连接回您的订单数据。 |
| `updated\_at` | 此列包含数据行上次更新的时间。 |

{style=&quot;table-layout:auto&quot;}
