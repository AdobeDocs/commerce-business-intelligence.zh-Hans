---
title: 需要[!DNL Google ECommerce]数据
description: 了解与Google E-commerce共享的数据类型。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# 预期[!DNL Google ECommerce]数据

在您的[!DNL Google ECommerce]帐户成功连接到[!DNL Commerce Intelligence]后，系统将开始将数据导入标题为`ecommerce`的表中。 此表记录每个事务处理的数据行。 这包括以下订单级数据列：

| 列名称 | 描述 |
|-----|-----|
| `\_id` | 此列是主键。 |
| `accountId` | 此列包含与您的[!DNL Google Analytics]电子商务帐户关联的帐户ID。 |
| `profileName` | 此列包含您的[!DNL Google Analytics]配置文件名称。 |
| `profileId` | 此列包含您的[!DNL Google Analytics]配置文件ID。 |
| `socialNetwork` | 此列包含社交网络的名称（例如，[!DNL Facebook]或[!DNL YouTube]） |
| `campaign` | 此列包含促销活动名称（例如，[`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)）。 |
| `medium` | 此列包含媒体名称（例如，[`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `source` | 此列包含源名称。 （例如，[`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `keyword` | 此列包含关键字说明（例如，[`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `transactionId` | 此列包含订单ID。 这用于将反向链接数据联接回您的订单数据。 |
| `updated\_at` | 此列包含上次更新数据行的时间。 |

{style="table-layout:auto"}
