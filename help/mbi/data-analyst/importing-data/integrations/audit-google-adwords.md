---
title: 审核Google Adwords数据
description: 了解导出Google Adwords数据的步骤。
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 审核[!DNL Google Adwords]数据

在[[!DNL Google Adwords]](../integrations/google-adwords.md)中发现一些奇怪的内容？ 要查明问题，您需要浏览数据。 可以通过将[!DNL Google Adwords]数据导出到`.csv`文件来完成此操作。

1. 下载并安装免费的[[!DNL Google Adwords] 编辑器](https://ads.google.com/home/tools/ads-editor/)应用程序。

1. 安装完成后，在`Add/manage accounts`面板中选择`Add Count`。

1. 输入您的[!DNL Google Adwords]帐户信息。

1. 将您的帐户添加到[!DNL Google Adwords]编辑器后，选择&#x200B;**[!UICONTROL File** > **&#x200B;导出电子表格(CSV)**> **导出整个帐户]**

这将生成一个`.csv`文件，其中包含存储在您当前[!DNL Google Adwords]帐户中的所有信息。 此时，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans) （请确保附加此文件！） 以便更仔细地查看您的数据。 如果文件太大，请通过[!DNL Dropbox]或[!DNL Google Drive]与[!DNL Commerce Intelligence]团队共享。

有关[!DNL Google Adwords] `.csv`文件导出的详细信息，请参阅官方的[[!DNL Google Adwords] 文档](https://support.google.com/google-ads/editor/answer/38657?hl=en)。
