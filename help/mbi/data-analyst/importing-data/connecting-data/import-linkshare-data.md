---
title: 导入Linkshare数据
description: 了解如何将Linkshare数据导入[!DNL Commerce Intelligence]。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%
---
# 导入[!DNL Linkshare]数据

要将您的[!DNL Linkshare]数据纳入[!DNL Adobe Commerce Intelligence]，您需要执行两项操作：

1. [以`.csv`格式导出Linkshare数据](#export)
1. [将电子表格上载到 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## 从Linkshare导出数据 {#export}

1. 在您的[!DNL Linkshare]帐户中，转到&#x200B;**[!UICONTROL Reports** > **Run Reports]。**

1. 在`Report`下拉列表中，选择&#x200B;**[!UICONTROL Sales & Activity Report]**。

1. 将所有其他下拉选项保留为默认选项。

1. 在`Date Range`下拉列表中，选择与[!DNL Commerce Intelligence]中的`Start of Week`设置匹配的任何选项(`Sun - Sat`、`Mon - Sun`)。

1. 清除`Compare Year-Over-Year Data`复选框。

1. 在`Data Type`下，选择`Transaction Date`。

   ![导入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 单击&#x200B;**[!UICONTROL View Report]**。

1. 单击&#x200B;**[!UICONTROL Download]**。

   此时，已下载一个`.csv`文件。

下载文件后，您可以使用[`File Upload`功能](../connecting-data/using-file-uploader.md)将其上传到[!DNL Commerce Intelligence]。
