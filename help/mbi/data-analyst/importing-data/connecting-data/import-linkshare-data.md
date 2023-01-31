---
title: 导入Linkshare数据
description: 了解如何将Linkshare数据导入 [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 导入 `Linkshare` 数据

将 `Linkshare` 数据输入 [!DNL MBI]，您需要执行两项操作：

1. [在中导出Linkshare数据 ](#export)
1. [将电子表格上传到 [!DNL MBI]](../connecting-data/using-file-uploader.md)

## 从Linkshare导出数据 {#export}

1. 在 `Linkshare` 帐户，转到 **[!UICONTROL Reports** > **Run Reports].**

1. 在 `Report` 下拉列表，选择 **[!UICONTROL Sales & Activity Report]**.

1. 将所有其他下拉选项保留为默认选项。

1. 在 `Date Range` 下拉菜单，选择选项(`Sun - Sat`, `Mon - Sun`与 `Start of Week` 设置 [!DNL MBI].

1. 清除 `Compare Year-Over-Year Data` 复选框。

1. 在 `Data Type`，选择 `Transaction Date`.

   ![导入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 单击 **[!UICONTROL View Report]**.

1. 单击 **[!UICONTROL Download]**.

   此时， `.csv` 文件。

下载文件后，您可以将其上传到 [!DNL MBI] 使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md).
