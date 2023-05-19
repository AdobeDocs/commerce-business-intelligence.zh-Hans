---
title: 匯入CJ Affiliate (Commission Junction)行銷資料
description: 瞭解如何將CJ Affiliate (Commission Junction)資料匯入 [!DNL Commerce Intelligence].L Commerce Intelligence]。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 匯入 [!DNL CJ Affiliate] 資料

匯入 [!DNL CJ Affiliate (Commission Junction)] 資料匯入 [!DNL Adobe Commerce Intelligence]，只需遵循下列步驟，並將產生的檔案附加至 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe會設定您帳戶的資料表，並允許您繼續獨立上傳資料。

## 匯出 [!DNL CJ Affiliate] 資料

1. 在您的 [!DNL CJ Affiliate] 帳戶，前往 `Reports` 標籤。

1. 在 `Performance` 索引標籤，選取 `Report Options`.

1. 設定 `Performance By` 等於 `Program`， `Trend` 等於 `Daily`、和 `Date Range` 等於要稽核的日期範圍。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選取 `Run Report`.

1. 在 `File Format` 下拉式清單，選取 `CSV`.  按一下 **[!UICONTROL Download]**.

   ![匯出cj附屬機構資料](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下載檔案後，您可以 [上傳檔案](../connecting-data/using-file-uploader.md) 至您的 [!DNL Commerce Intelligence] Data Warehouse。

   這樣會在中建立表格 [!DNL Commerce Intelligence] 可繼續定期將最新資料上傳至的Data Warehouse。 上傳檔案時，請遵循下列格式要求： [使用檔案上傳程式](../connecting-data/using-file-uploader.md).
