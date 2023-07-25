---
title: 导入MailChimp数据
description: 了解如何将MailChimp数据导入 [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 导入 [!DNL Mailchimp] 数据

要全面了解您的营销活动，您可以导入 [!DNL Mailchimp] 通过电子邮件将营销活动数据发送至 [!DNL Commerce Intelligence]. 要完成导入，您需要为每个导入执行以下操作 [!DNL Mailchimp] 您的营销活动：

## 导出打开数据 {#opens}

1. 登录后 [!DNL Mailchimp]，转到 `Campaigns` 选项卡。

   ![导入mailchimp 1](../../../assets/import-mailchimp-1.png)

1. 单击 **[!UICONTROL View Report]**，位于营销活动名称旁边。

   ![导入mailchimp 2](../../../assets/import-mailchimp-2.png)

1. 单击 **[!UICONTROL Opened]** 数字。

   ![导入mailchimp 3](../../../assets/import-mailchimp-3.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您必须添加 `primary key`， `date (mm/dd/yyyy)`、和 `campaign name` 列添加到该文件中。 确保 `primary keys` 对于每一行都是唯一的。

   ![导入mailchimp 4](../../../assets/import-mailchimp-4.png)

## 导出点击量数据 {#clicks}

1. 导航回到 `View Report` 屏幕查看营销活动。

1. 单击该数字 `Clicked`.

   ![导入mailchimp 5](../../../assets/import-mailchimp-5.png)

1. 单击 `Total Clicks` 或 `Unique Clicks` 列。

   ![导入mailchimp 6](../../../assets/import-mailchimp-6.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您必须添加 `Primary Key`， `date (mm/dd/yyyy)`， `campaign name`、和 `URL` 列添加到该文件中。 您无需添加完整URL，只需添加一些让您知道点击了什么内容的内容。

   ![导入mailchimp 7](../../../assets/import-mailchimp-7.png)

1. 对电子邮件中点击的每个URL重复步骤3和4，将所有数据组合到同一个中 `.csv` 文件完成。

## 导出发送的数据 {#sent}

1. 进入 `Campaigns` 选项卡/ [!DNL Mailchimp].

1. 单击 **[!UICONTROL View Report]** 在营销活动名称旁边。

1. 单击旁边的数字 `Recipients`.

   ![导入mailchimp 8](../../../assets/import-mailchimp-8.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您必须添加 `Primary Key`， `date (mm/dd/yyyy)`、和 `campaign name` 列添加到该文件中。

   ![导入mailchimp 9](../../../assets/import-mailchimp-9.png)

## 准备文件以上传到 [!DNL Commerce Intelligence] {#upload}

每个文件 —  `Opens`， `Clicks`、和 `Sent`  — 应上传到 [!DNL Commerce Intelligence] 作为单独的文件。 Adobe建议使用以下命名约定来命名文件： `MailChimp\_ACTION\_DATE`. Replace `ACTION` 替换为 `Open`， `Click`，或 `Sent`，并替换 `DATE` 带有导出日期。

当您准备好上传文件时，请使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 将数据导入您的Data warehouse。
