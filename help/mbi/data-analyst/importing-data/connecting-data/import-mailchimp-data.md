---
title: 匯入MailChimp資料
description: 瞭解如何將MailChimp資料匯入 [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 匯入 [!DNL Mailchimp] 資料

若要全面瞭解您的行銷活動，您可以匯入 [!DNL Mailchimp] 透過電子郵件將行銷活動資料傳送至 [!DNL Commerce Intelligence]. 若要完成匯入，您需要針對每個 [!DNL Mailchimp] 您的行銷活動：

## 匯出開啟的資料 {#opens}

1. 登入之後 [!DNL Mailchimp]，前往 `Campaigns` 標籤。

   ![匯入mailchimp 1](../../../assets/import-mailchimp-1.png)

1. 按一下 **[!UICONTROL View Report]**，促銷活動名稱旁。

   ![匯入mailchimp 2](../../../assets/import-mailchimp-2.png)

1. 按一下 **[!UICONTROL Opened]** 數字。

   ![匯入mailchimp 3](../../../assets/import-mailchimp-3.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `primary key`， `date (mm/dd/yyyy)`、和 `campaign name` 欄放入此檔案。 確定 `primary keys` 每一列都是唯一的。

   ![匯入mailchimp 4](../../../assets/import-mailchimp-4.png)

## 匯出點選資料 {#clicks}

1. 導覽回至 `View Report` 行銷活動的畫面。

1. 按一下符合以下條件的數字 `Clicked`.

   ![匯入mailchimp 5](../../../assets/import-mailchimp-5.png)

1. 按一下 `Total Clicks` 或 `Unique Clicks` 欄。

   ![匯入mailchimp 6](../../../assets/import-mailchimp-6.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `Primary Key`， `date (mm/dd/yyyy)`， `campaign name`、和 `URL` 欄放入此檔案。 您不需要新增完整URL，只要讓您知道點選了什麼即可。

   ![匯入mailchimp 7](../../../assets/import-mailchimp-7.png)

1. 對電子郵件中按下的每個URL重複步驟3和4，將所有資料合併到相同檔案中 `.csv` 檔案完成時。

## 匯出已傳送的資料 {#sent}

1. 前往 `Campaigns` 索引標籤/ [!DNL Mailchimp].

1. 按一下 **[!UICONTROL View Report]** 位於行銷活動名稱旁。

1. 按一下旁邊的數字 `Recipients`.

   ![匯入mailchimp 8](../../../assets/import-mailchimp-8.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `Primary Key`， `date (mm/dd/yyyy)`、和 `campaign name` 欄放入此檔案。

   ![匯入mailchimp 9](../../../assets/import-mailchimp-9.png)

## 準備檔案以上傳到 [!DNL Commerce Intelligence] {#upload}

每個檔案 —  `Opens`， `Clicks`、和 `Sent`  — 應上傳至 [!DNL Commerce Intelligence] 作為單獨的檔案。 Adobe建議您使用此命名慣例來命名檔案： `MailChimp\_ACTION\_DATE`. Replace `ACTION` 替換為 `Open`， `Click`，或 `Sent`，並取代 `DATE` 包含匯出日期。

當您準備好上傳檔案時，請使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 將資料帶入您的Data Warehouse。
