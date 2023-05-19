---
title: 資料和更新資訊
description: 瞭解如何檢查更新週期的狀態。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 資料和更新資訊

* [我的資料為何變更？](#datachange)
* [定期和強制更新之間有何差異？](#regularforcedupdates)
* [更新週期為何需要很長時間？](#updatecycletime)
* [更新週期完成時是否可以通知我？](#notifyupdate)
* [為什麼是 [!DNL Google ECommerce] 資料與我的資料庫不同？](#ecommdatabase)
* [如何疑難排解資料差異？](#datadiscrepancy)

## 我的資料為何變更？ {#datachange}

圖表值會因新資料同步至您的Data Warehouse而在一天中不斷變更。 此外，現有資料欄的值可能因為 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md). 重新檢查是在資料欄中尋找變更值的程式，例如從移出的訂單狀態 `open` 至 `shipped`.

有幾種不同的方式 [檢查更新週期的狀態](../../best-practices/check-update-cycle.md)，視使用者的許可權設定而定。

## 定期和強制更新之間有何差異？ {#regularforcedupdates}

定期更新包括 **已排程** 強制更新時的程式 **由您啟動的手動處理**. 如果您有中斷時數(或時間段，其中 [!DNL Commerce Intelligence] 不應更新您的資料)，強制更新會啟動一個不遵守中斷期間限制的週期。

## 更新週期為何需要很長時間？ {#updatecycletime}

許多因素都會增加原本就漫長的更新時間。 特定 [復寫方法](../data-warehouse-mgr/cfg-replication-methods.md)， [較高的重新檢查頻率](../data-warehouse-mgr/cfg-data-rechecks.md)，而控制面板和圖表的數量只是少數幾個貢獻者。 Adobe建議 [重新設定部分設定](../../best-practices/reduce-update-cycle-time.md) 和 [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md) 以縮短更新時間。

## 更新週期完成時是否可以通知我？ {#notifyupdate}

如果更新進行中，則連結會位於 `Connections` 週期完成時，可用於請求電子郵件通知的頁面。

## 為什麼是[!DNL Google ECommerce]資料與我的資料庫不同？ {#ecommdatabase}

兩者之間的差異 [!DNL Google Analytics] 和資料庫可能會因為各種原因而產生。 無法正確啟用追蹤、使用者造訪無痕以及點選事件無法正常運作只是幾個範例。 如果您的收入和訂單看起來不正確， [請參閱此主題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 以診斷問題。

## 如何疑難排解資料差異？ {#datadiscrepancy}

Adobe知道看到不一致的資料可能會讓人感到沮喪。 嘗試使用 [資料差異檢查清單](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) 或 [資料匯出教學課程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) 以診斷問題。 如果您仍然被截斷， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
