---
title: 导入Linkshare数据
description: 了解如何将Linkshare数据导入 [!DNL Commerce Intelligence]。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
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

1. 在`Date Range`下拉列表中，选择与[!DNL Commerce Intelligence]中的`Start of Week`设置匹配的任何选项(`Sun - Sat`、`Mon - Sun`)。

1. 清除`Compare Year-Over-Year Data`复选框。

1. 在`Data Type`下，选择`Transaction Date`。

   ![导入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 单击&#x200B;**[!UICONTROL View Report]**。

1. 单击&#x200B;**[!UICONTROL Download]**。

   此时，已下载一个`.csv`文件。

下载文件后，您可以使用[`File Upload`功能](../connecting-data/using-file-uploader.md)将其上传到[!DNL Commerce Intelligence]。
