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

# 数据验证 [!DNL Mixpanel]

时间 [!DNL Adobe Commerce Intelligence] 首先连接到 [!DNL Mixpanel] 数据，您的客户经理或分析师可能会要求您提供数据导出来自 [!DNL Mixpanel] 用于验证目的。 这样，您可以确认已同步了所有可直接在中使用的相同数据 [!DNL Mixpanel].

## 数据导出过程： `Events`

1. 访问您的 `Segmentation` 截面和视图 `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. 选择 `Past 96 Hours` 在时间范围内

   ![](../../../assets/past-96-hours.png)

1. 滚动到报告的右下部分并导出 `.csv` 文件：

   ![](../../../assets/export-csv-mixpanel.png)

1. 发送 `.csv` 文件发送给在此验证流程中与之合作的客户经理或分析师。
