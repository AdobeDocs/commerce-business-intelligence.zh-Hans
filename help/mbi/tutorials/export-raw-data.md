---
title: 匯出原始資料
description: 瞭解如何從匯出記錄 [!DNL Commerce Intelligence] Data Warehouse以進一步瞭解為您的儀表板提供動力的內容。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 匯出原始資料

使用原始資料匯出，您可以匯出Data Warehouse中的記錄，以更近距離地瞭解為您的儀表板提供支援的功能。 此外，原始資料匯出也可協助您 [精準的資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

原始資料匯出可讓您存取透過非標準化及預先彙總相關量度而產生的其他欄和維度。 例如， `User's first order date` 是可為每個使用者匯出的維度 [!DNL Commerce Intelligence]，但資料庫中可能無法使用。

本教學課程涵蓋下列內容：

* [選取要匯出的資料](#select)
* [下載匯出(](#download)
* [存取歷史匯出](#historical)

## 步驟1：選取要匯出的資料 {#select}

有兩種方式可匯出原始資料 [!DNL Commerce Intelligence]：

1. 在圖表層級
1. 在表格層級

### 在中於表格層級匯出 [!UICONTROL Manage Data] 標籤

如果要匯出表格來源 [!UICONTROL Manage Data] 標籤，您需要 [管理員](../administrator/user-management/user-management.md) 許可權。

1. 按一下 **[!UICONTROL Manage Data** > **&#x200B;匯出資料&#x200B;**> **原始資料匯出]**.
1. 您會看到 `Export List` 最新建立的資料匯出專案（如果有的話）。 按一下 **[!UICONTROL Add Export]** 以建立匯出。
1. 此 `New Raw Data Export` 對話方塊隨即顯示。 在這裡，您可以透過選取或取消選取欄和篩選器來自訂匯出：

   * `Table` - `Table` 欄位會選取從中匯出資料的表格。 依預設，這會顯示您導覽至的表格。
   * `Export Name`  — 在此欄位中輸入匯出的名稱。 例如： `Philadelphia - Daily Revenue`.
   * `Available Columns`  — 此欄位會列出資料庫中可包含在匯出中的欄（維度）。 若要新增欄，請按一下其名稱。
   * `Selected Columns`  — 此欄位會列出目前包含在匯出中的欄（維度）。 若要移除欄，請按一下其名稱。
   * `Filter`  — 本節列出目前套用至匯出的篩選器。 這些篩選器可以變更；也可以新增篩選器以匯出特定資料集。
   * 完成後，按一下 **[!UICONTROL Export Data]**.

### 從控制面板在圖表層級匯出

1. 按一下任何圖表右上角的齒輪圖示。

1. 選取 `Raw Export` 以顯示 `Raw Export` 對話方塊。

1. 選擇「 」來自訂匯出 `table`， `columns`、和 `filters` 以包含或排除。 請參閱上一節，以取得此模組欄位的詳細資訊。

   >[!NOTE]
   >
   >顯示在「 」中的 `Table` 欄位預設為提供圖表支援的表格。

1. 完成後，按一下 **[!UICONTROL Export Data]**.

在圖表層級檢視整個程式。

![](../assets/Chart-level_export.gif)

## 步驟2：下載匯出 {#download}

完成您在「 」中的選取專案後，匯出就會立即開始處理 `Raw Data Export` 對話方塊。 由於部分匯出內容可能較大，因此限製為1,000萬列，且可能需要一些時間才能執行。

若要檢查匯出是否已就緒，請按一下 **[!UICONTROL Raw Data Exports]** 在畫面的右上角。 按一下 **[!UICONTROL Download]** 下載壓縮檔 `.csv` 匯出的檔案。

![](../assets/Downloading_export.gif)

## 步驟3：存取歷史匯出 {#historical}

若要檢視過去的匯出專案，請按一下 **[!UICONTROL Raw Data Export]** 在熒幕的右上角。 待定和已完成的報表最多可存取7天。
