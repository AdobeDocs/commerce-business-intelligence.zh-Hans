---
title: Mixpanel中的数据验证
description: 了解如何确认您已直接在Mixpanel中同步所有可用数据。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 134
ht-degree: 0%

---

# [!DNL Mixpanel]中的数据验证

当[!DNL Adobe Commerce Intelligence]首次连接到您的[!DNL Mixpanel]数据时，您的客户经理或分析师可能会请求您从[!DNL Mixpanel]提供数据导出以进行验证。 这允许您确认已同步直接在[!DNL Mixpanel]内对您可用的所有数据。

## 数据导出过程： `Events`

1. 访问您的`Segmentation`分区并查看`Your Top Events`。

   ![Mixpanel仪表板显示您的热门事件](../../../assets/your-top-events.png)

1. 为时间范围选择`Past 96 Hours`

   ![显示过去96小时的Mixpanel时间范围选择器选项](../../../assets/past-96-hours.png)

1. 滚动到报告的右下部分并导出`.csv`文件：

   ![菜单中的“Mixpanel导出为CSV”选项](../../../assets/export-csv-mixpanel.png)

1. 将`.csv`文件发送给在此验证过程中与您合作的客户经理或分析师。

