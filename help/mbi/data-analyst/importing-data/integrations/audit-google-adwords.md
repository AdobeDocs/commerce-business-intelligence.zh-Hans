---
title: 审核Google Adwords数据
description: 了解导出Google Adwords数据的步骤。
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/2M1Lo7m11aCB5GZrcnA7hQX1qqZ6DHPdAt9wesbfL98
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 0%

---

# 审核[!DNL Google Adwords]数据

在[[!DNL Google Adwords]](../integrations/google-adwords.md)中发现一些奇怪的内容？ 要查明问题，您需要浏览数据。 可以通过将[!DNL Google Adwords]数据导出到`.csv`文件来完成此操作。

1. 下载并安装免费的[[!DNL Google Adwords] 编辑器](https://ads.google.com/home/tools/ads-editor/)应用程序。

1. 安装完成后，在`Add Count`面板中选择`Add/manage accounts`。

1. 输入您的[!DNL Google Adwords]帐户信息。

1. 将您的帐户添加到[!DNL Google Adwords]编辑器后，选择&#x200B;**[!UICONTROL File** > **&#x200B;导出电子表格(CSV)**> **导出整个帐户]**

这将生成一个`.csv`文件，其中包含存储在您当前[!DNL Google Adwords]帐户中的所有信息。 此时，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （请确保附加此文件！），以便您可以更仔细地查看数据。 如果文件太大，请通过[!DNL Commerce Intelligence]或[!DNL Dropbox]与[!DNL Google Drive]团队共享。

有关[!DNL Google Adwords] `.csv`文件导出的详细信息，请参阅官方的[[!DNL Google Adwords] 文档](https://support.google.com/google-ads/editor/answer/38657?hl=en)。
