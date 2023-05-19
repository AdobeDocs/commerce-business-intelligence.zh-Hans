---
title: 格式化和匯入財務資料
description: 瞭解如何格式化和匯入財務資料。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 格式化和匯入財務資料

本主題討論匯入財務資料以便在中分析的最佳方式 [!DNL Adobe Commerce Intelligence].

二維交叉表資料表格通常是財務資料使用的格式。 藉由欄和列中的標籤分類值，這種版面配置可能很容易透過人眼和試算表工具檢視，但對資料庫不友好。

![](../../mbi/assets/crosstab.png)

若要在中匯入和分析此資料 [!DNL Commerce Intelligence]，表格必須平面化為一維清單。 平面化時，每個資料值會依多個標籤分類，這些標籤全都位在單一列中，其中每一列都是唯一的，或是會有唯一的識別碼，例如主索引鍵欄。

![](../../mbi/assets/flattened.png)

## 格式化要匯入的Excel檔案

若要使用 [!DNL Excel] 樞紐分析表：

1. 使用二維資料表開啟檔案。
1. 開啟樞紐分析表精靈。 在 [!DNL Windows]，捷徑為 `Alt-D`. 在 [!DNL Mac OS]，輸入 `Command-Option-P`.
1. 選取 **[!UICONTROL Multiple consolidated ranges]** 並按一下 **[!UICONTROL Next]**.
1. 選取 **[!UICONTROL I will create the page fields]** 並按一下 **[!UICONTROL Next]**.
1. 選取二維表格中的整個資料集，包括標籤。 確定 `0` 選取所需頁面欄位的數量，然後按一下 **[!UICONTROL Next]**.
1. 在新工作表中建立樞紐分析表，然後按一下 **[!UICONTROL Finish]**.
1. 從欄位清單中取消選取欄和列欄位。
1. 連按兩下產生的數值，在新頁面中顯示展平的來源資料。
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 另存新檔 `CSV` 檔案。

## 正在結束

資料表格已轉換為清單格式，保留其所有原始資訊，現在可以 [匯入至 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 以進行分析。
