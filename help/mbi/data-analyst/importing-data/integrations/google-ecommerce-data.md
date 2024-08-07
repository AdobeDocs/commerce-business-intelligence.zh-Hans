---
title: 需要[!DNL Google ECommerce]数据
description: 了解与Google E-commerce共享的数据类型。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
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
