---
title: 导入CJ附属机构（佣金联合）营销数据
description: 了解如何将CJ附属活动(Commission Junction)数据导入 [!DNL Commerce Intelligence].L Commerce Intelligence。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# 导入[!DNL CJ Affiliate]数据

要将[!DNL CJ Affiliate (Commission Junction)]数据导入[!DNL Adobe Commerce Intelligence]，只需执行以下步骤并将结果文件附加到[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)即可。 Adobe将为您的帐户设置数据表，并允许您继续独立上传数据。

## 导出[!DNL CJ Affiliate]数据

1. 在您的[!DNL CJ Affiliate]帐户中，转到`Reports`选项卡。

1. 在`Performance`选项卡中，选择`Report Options`。

1. 将`Performance By`设置为等于`Program`，`Trend`设置为等于`Daily`，`Date Range`设置为等于要审核的日期范围。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 选择`Run Report`。

1. 在`File Format`下拉列表中，选择`CSV`。  单击&#x200B;**[!UICONTROL Download]**。

   ![导出cj附属活动数据](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下载文件后，您可以[将该文件](../connecting-data/using-file-uploader.md)上传到您的[!DNL Commerce Intelligence] Data Warehouse。

   这会在[!DNL Commerce Intelligence] Data Warehouse中创建一个表，您可以定期继续将新数据上传到该表中。 上载文件时，请遵循[使用文件上载程序](../connecting-data/using-file-uploader.md)中列出的格式要求。
