---
title: 导入MailChimp数据
description: 了解如何将MailChimp数据导入 [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 导入 `MailChimp` 数据

要全面了解您的竞选活动工作，您可以导入 `MailChimp` 电子邮件促销活动数据输入到 [!DNL MBI]. 要完成导入，您需要对 `MailChimp` 您拥有的营销活动：

## 导出打开数据 {#opens}

1. 登录后 `MailChimp`，转到 `Campaigns` 选项卡。

   ![导入mailchimp 1](../../../assets/import-mailchimp-1.png)

1. 单击 **[!UICONTROL View Report]**，位于营销活动名称旁边。

   ![导入mailchimp 2](../../../assets/import-mailchimp-2.png)

1. 单击 **[!UICONTROL Opened]** 数字。

   ![导入mailchimp 3](../../../assets/import-mailchimp-3.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您需要添加 `primary key`, `date (mm/dd/yyyy)`和 `campaign name` 列。 确保 `primary keys` 对于每行都是唯一的。

   ![导入mailchimp 4](../../../assets/import-mailchimp-4.png)

## 导出点击数据 {#clicks}

1. 导航回 `View Report` 屏幕。

1. 单击 `Clicked`.

   ![导入mailchimp 5](../../../assets/import-mailchimp-5.png)

1. 单击 `Total Clicks` 或 `Unique Clicks` 列。

   ![导入mailchim 6](../../../assets/import-mailchimp-6.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您需要添加 `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`和 `URL` 列。 您无需添加完整的URL，只需添加一些内容即可了解已点击的内容。

   ![导入mailchimp 7](../../../assets/import-mailchimp-7.png)

1. 对电子邮件中点击的每个URL重复步骤3和4，将所有数据合并到同一个 `.csv` 文件时。

## 导出发送的数据 {#sent}

1. 进入 `Campaigns` 选项卡。

1. 单击 **[!UICONTROL View Report]** 营销活动名称旁边。

1. 单击旁边的数字 `Recipients`.

   ![导入mailchimp 8](../../../assets/import-mailchimp-8.png)

1. 单击 **[!UICONTROL Export]** 并保存 `.csv` 文件。

   您需要添加 `Primary Key`, `date (mm/dd/yyyy)`和 `campaign name` 列。

   ![导入mailchimp 9](../../../assets/import-mailchimp-9.png)

## 准备要上传到的文件 [!DNL MBI] {#upload}

每个文件 —  `Opens`, `Clicks`和 `Sent`  — 应上传到 [!DNL MBI] 作为单独的文件。 我们还建议您使用此命名约定命名文件： `MailChimp\_ACTION\_DATE`. 替换 `ACTION` with `Open`, `Click`或 `Sent`，替换 `DATE` 和导出日期。

准备好上传文件后，请使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 将数据导入data warehouse。
