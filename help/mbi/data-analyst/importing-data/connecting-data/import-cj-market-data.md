---
title: 导入CJ关联（佣金结）营销数据
description: 了解如何将CJ Affiliate(Commission Junction)数据导入 [!DNL MBI].L MBI]。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 导入 `CJ Affiliate` 数据

导入 `CJ Affiliate` （委员会连接）数据输入 [!DNL MBI]，只需按照以下步骤操作，并将生成的文件附加到支持票证即可。 我们将设置您的帐户的数据表，并允许您继续单独上传数据。

## 导出 `CJ Affiliate` 数据

1. 在 `CJ Affiliate` 帐户，转到 `Reports` 选项卡。

1. 在 `Performance` 选项卡，选择 `Report Options`.

1. 已设置 `Performance By` 等于 `Program`, `Trend` 等于 `Daily`和 `Date Range` 等于审核的日期范围。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 选择 `Run Report`.

1. 在 `File Format` 下拉列表，选择 `CSV`.  单击 **[!UICONTROL Download]**.

   ![导出cj附属数据](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下载文件后，您可以 [上传文件](../connecting-data/using-file-uploader.md) 至 [!DNL MBI] data warehouse。

   这会在 [!DNL MBI] data warehouse，您可以继续定期将新数据上传到。 上传文件时，请确保遵循 [使用文件加载器](../connecting-data/using-file-uploader.md).
