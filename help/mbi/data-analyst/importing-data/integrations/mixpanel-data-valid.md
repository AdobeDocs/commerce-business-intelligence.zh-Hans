---
title: Mixpanel中的数据验证
description: 了解如何确认您已直接在Mixpanel中同步所有可用数据。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!DNL Mixpanel]中的数据验证

当[!DNL Adobe Commerce Intelligence]首次连接到您的[!DNL Mixpanel]数据时，您的客户经理或分析师可能会请求您从[!DNL Mixpanel]提供数据导出以进行验证。 这允许您确认已同步直接在[!DNL Mixpanel]内对您可用的所有数据。

## 数据导出过程： `Events`

1. 访问您的`Segmentation`分区并查看`Your Top Events`。

   ![](../../../assets/your-top-events.png)

1. 为时间范围选择`Past 96 Hours`

   ![](../../../assets/past-96-hours.png)

1. 滚动到报告的右下部分并导出`.csv`文件：

   ![](../../../assets/export-csv-mixpanel.png)

1. 将`.csv`文件发送给在此验证过程中与您合作的客户经理或分析师。
