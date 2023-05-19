---
title: 縮短更新週期時間
description: 瞭解如何縮短更新週期時間。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 縮短更新週期處理時間

[!DNL Adobe Commerce Intelligence] 一整天都會與您的資料庫同步，以複製新資料，確保您的儀表板一律顯示最新資訊。

許多因素都會增加原本就漫長的更新時間。 某些複製方法、較高的重新檢查頻率以及儀表板和圖表數量只是少數幾個因素。 本主題說明縮短更新時間的一些最佳實務。

## 降低重新檢查頻率

在資料庫表格中，可以有具有可變值的資料欄。 例如，在 **訂購** 表格中可能有一個名為的欄 **狀態**. 最初將訂單寫入資料庫時，狀態列可能包含值 `pending`. 訂單會複製到您的 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) 與此 `pending` 值。

可變更的欄必須是 [已重新檢查更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 隨著時間推移。 依預設， [!DNL Commerce Intelligence] 在每次更新期間都會重新檢查這些欄，但如果要重新檢查和復寫大量資料，可能會對更新時間造成負面影響。 Adobe建議將重新檢查頻率設定為每日、每週或每月，而不是在每次更新時執行重新檢查。

## 使用增量複製方法

如上所述，長的更新時間與必須重新檢查及復寫多少資料直接相關。 [增量複製方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 可大幅減少更新週期中處理的資料量。 Adobe建議儘可能使用這些方法，或修改資料庫以支援增量方法。

## 從儀表板移除未使用的圖表

在更新週期結束時， [!DNL Commerce Intelligence] 對所有圖表執行快取作業。 快取會儲存資料，以便日後能更快速地完成資訊請求。 在 [!DNL Commerce Intelligence]，這表示儀表板載入迅速，因為圖表不需要在每次載入時查詢資料。

從 [!DNL Commerce Intelligence] 僅對儀表板中找到的圖表執行快取操作，從儀表板中移除未使用的圖表會減少更新時間。 請記住，同一圖表可能位於多個儀表板上 — 請洽詢您的團隊，確保他們也會移除任何未使用的圖表。

>[!NOTE]
>
>從儀表板中移除圖表並不會刪除圖表。 您可以 [隨時重新新增](../data-user/dashboards/add-charts-dashboard.md).

## 最佳化資料庫以進行分析

除了重新評估重新檢查頻率、複製方法和圖表有用性之外，您還可以 [最佳化資料庫以供分析](../best-practices/opt-db-analysis.md).

## 正在結束

如果實施這些建議後更新時間仍顯緩慢， [聯絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
