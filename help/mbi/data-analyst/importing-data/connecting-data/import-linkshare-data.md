---
title: 导入Linkshare数据
description: 了解如何将Linkshare数据导入 [!DNL Commerce Intelligence]。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 0%

---

# 导入[!DNL Linkshare]数据

要将您的[!DNL Linkshare]数据纳入[!DNL Adobe Commerce Intelligence]，您需要执行两项操作：

1. [在中导出Linkshare数据 ](#export)
1. [将电子表格上载到 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## 从Linkshare导出数据 {#export}

1. 在您的[!DNL Linkshare]帐户中，转到&#x200B;**[!UICONTROL Reports** > **Run Reports]。**

1. 在`Report`下拉列表中，选择&#x200B;**[!UICONTROL Sales & Activity Report]**。

1. 将所有其他下拉选项保留为默认选项。

1. 在`Date Range`下拉列表中，选择与`Sun - Sat`中的`Mon - Sun`设置匹配的任何选项(`Start of Week`、[!DNL Commerce Intelligence])。

1. 清除`Compare Year-Over-Year Data`复选框。

1. 在`Data Type`下，选择`Transaction Date`。

   ![导入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 单击&#x200B;**[!UICONTROL View Report]**。

1. 单击&#x200B;**[!UICONTROL Download]**。

   此时，已下载一个`.csv`文件。

下载文件后，您可以使用[!DNL Commerce Intelligence]功能[`File Upload`将其上传到](../connecting-data/using-file-uploader.md)。
