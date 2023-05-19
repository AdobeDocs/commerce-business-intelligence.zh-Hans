---
title: 預期 [!DNL Adobe Analytics] 資料
description: 瞭解連線您的RDS執行個體的步驟。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 預期 [!DNL Adobe Analytics] 資料

此 [!DNL Adobe Analytics] 整合 [!DNL Adobe Commerce Intelligence] 使用 [Analytics 2.0報表API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>為確保您取得預期的資料，您可以先在中建立報表 [!DNL Adobe Analytics] 具有所需量度和維度的工作區。 這可讓您檢查資料的相容性和可用性。

每個已連線的報表套裝有一個資料表呼叫 `report-suite-<ID>` (其中 `<ID>` 是由產生的唯一ID [!DNL Commerce Intelligence])中建立的Data Warehouse。

此表格的結構描述是由您在整合設定程式中選取的量度和維度所組成。 還會產生其他數個欄 [!DNL Commerce Intelligence]，用於識別身分。

例如，如果您在設定期間選取下列量度和維度：
- `Metric`: `Page views`
- `Dimension`: `Page`

此表格將包含下列欄：

| 欄名稱 | 說明 |
| --- | --- |
| `_id` | 此欄是主索引鍵。 |
| `_item_hash` | [!DNL Commerce Intelligence] 唯一識別碼。 此欄的建立者 [!DNL Commerce Intelligence]. |
| `_updated_at` | 此欄包含上次更新資料列的時間。 建立者： [!DNL Commerce Intelligence]. |
| `start_date` | 列中包含資料的開始日期。 `start_date` 一列中永遠是同一天的00:00。 |
| `end_date` | 列所包含資料的結束日期。 `end_date` 一列中永遠是同日23:59。 |
| `page_views` | 選取的量度：所識別時段內的頁面檢視總數。 |
| `page` | 選取的維度：具有追蹤檢視的個別頁面名稱。 |

控制哪些選取的量度和維度可在您的 [!DNL Commerce Intelligence] 表格範例使用 *同步* 或 *取消同步* 中的選項 `Data Warehouse` 頁面。 目前未同步的欄會以灰色顯示。 如果您停止同步欄，可以稍後再次開始同步。

## 目前限制

本節概述 [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence].

| 限制 | 說明 |
| --- | --- |
| `Historical data period` | 如同其他協力廠商整合， [!DNL Adobe Analytics] 整合會提取有限的歷史資料量，然後繼續更新資料。 歷史期間設定為2週。 |
| `Empty component combinations` | 某些量度和維度組合沒有包含資料。 如果選取這種組合進行復寫， [!DNL Commerce Intelligence] 會從複製的表格中排除資料行。 若要避免選取這類組合，您可以先在 [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) 以確認您取得預期的資料。 |
| `Re-authorization cadence` | 重新授權 [!DNL Adobe Analytics] 每兩週需要整合一次。 若要重新授權，請前往整合的「編輯」頁面，然後按一下 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] 一次提供一個維度的量度資料。 如果您在設定期間選取多個維度，則在 [!DNL Commerce Intelligence] 表格包含單一維度值，且每個維度都為null。 |
