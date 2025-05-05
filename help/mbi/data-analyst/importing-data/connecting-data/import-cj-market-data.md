---
title: 导入CJ附属机构（佣金联合）营销数据
description: 了解如何将CJ附属活动(Commission Junction)数据导入 [!DNL Commerce Intelligence].L Commerce Intelligence。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 导入[!DNL CJ Affiliate]数据

要将[!DNL CJ Affiliate (Commission Junction)]数据导入[!DNL Adobe Commerce Intelligence]，只需执行以下步骤并将结果文件附加到[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)即可。 Adobe将设置您帐户的数据表，并允许您继续独立上传数据。

## 导出[!DNL CJ Affiliate]数据

1. 在您的[!DNL CJ Affiliate]帐户中，转到`Reports`选项卡。

1. 在`Performance`选项卡中，选择`Report Options`。

1. 将`Performance By`设置为等于`Program`，`Trend`设置为等于`Daily`，`Date Range`设置为等于要审核的日期范围。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 选择`Run Report`。

1. 在`File Format`下拉列表中，选择`CSV`。  单击&#x200B;**[!UICONTROL Download]**。

   ![导出cj附属活动数据](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下载文件后，您可以[将文件](../connecting-data/using-file-uploader.md)上传到您的[!DNL Commerce Intelligence]Data Warehouse。

   这会在[!DNL Commerce Intelligence]Data Warehouse中创建一个表，您可以继续定期将新数据上传到该表中。 上载文件时，请遵循[使用文件上载程序](../connecting-data/using-file-uploader.md)中列出的格式要求。
