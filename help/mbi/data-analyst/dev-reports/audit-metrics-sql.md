---
title: 使用SQLReport Builder
description: 瞭解如何使用SQLReport Builder稽核資料和測量結果，以便將結果與本機資料庫的資料進行比較。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

此 [!DNL SQL Report Builder] 主要用於建立新報告和疊代分析，但也可用於有效稽核資料和量度。 以下資訊說明如何使用 [!DNL SQL Report Builder] 以便將結果與本機資料庫的資料進行比較。

## 查詢量度

若要開始使用，請開啟 [!DNL SQL Report Builder] 瀏覽至 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. 您可以使用中的側欄 [!DNL SQL] 編輯器，將游標移至量度上並按一下「 」，直接將量度插入查詢 **[!UICONTROL Insert]**. 這會將該量度的查詢定義新增至編輯器。 此定義包含下列元件：

- 此 **量度作業** 正在執行，指示為 `SUM()` 在以下範例中。
- 此 **表格於** 建立量度的位置，由以下專案指示： `FROM` 子句。
- 任何 **篩選器（和篩選器集）** 已新增至量度的資訊，由以下所示： `WHERE` 子句。
- 的元件 **timestamp** 要訂購資料的（年、月），由 `ORDER BY` 子句。

若要更清楚的檢視查詢，您可以重新格式化查詢欄位中的顯示方式。 準備就緒後，選擇 `Run Query`. 結果會填入查詢下方報表面板中的表格中。

![](../../assets/run-query-results.gif)

## 限制查詢

如果您嘗試查明特定差異或資料集，您應該將查詢限製為特定範例，以對照您的本機資料庫檢查。 您可以編輯查詢以符合所需的限制來完成此操作。 在下列範例中，您限制查詢僅包含來自2013年1月1日或之後日期的收入。 更新查詢後，選取 **[!UICONTROL Run Query]** 以更新結果。

![](../../assets/restricting-query.gif)

## 儲存和匯出

當報表符合您的需求時，請為報表指定不同的名稱，然後按一下 **[!UICONTROL Save]**，並選取您要儲存的報表型別和控制面板。 稽核量度時，Adobe建議將報表儲存為 `Table` 並儲存至測試儀表板。

儲存報告後，選取「 」，導覽至該儀表板 `Go to Dashboard`. 從那裡，您可以尋找報告並選取 **[!UICONTROL Options gear > Full `.csv`匯出]** 或 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 自訂查詢

您也可以撰寫自訂查詢並匯出結果，以便與本機資料庫進行比較。 遵循 [查詢最佳化准則](../../best-practices/optimizing-your-sql-queries.md)，在SQL編輯器中撰寫查詢。 您可以使用側邊欄頂端的按鈕，在表格清單與可用於的量度之間切換 [!DNL SQL Report Builder] 並將它們新增至您的查詢。 當自訂查詢符合您的需求時，您可以儲存報告並從儀表板匯出該資料。

>[!NOTE]
>
>如果稽核資料後發現不一致，請檢視 [連絡支援：資料差異](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 支援主題以取得後續操作的相關資訊。
