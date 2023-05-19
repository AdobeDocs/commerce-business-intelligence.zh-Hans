---
title: 設定資料檢查
description: 瞭解如何使用可變更的值設定資料欄。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 設定資料檢查

在資料庫表格中，可以有具有可變值的資料欄。 例如，在 `orders` 表格中可能有一個名為的欄 `status`. 最初將訂單寫入資料庫時，狀態列可能包含值 _擱置中_. 訂單會複製到您的 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) 與此 `pending` 值。

訂單狀態可以變更，但並不一定在 `pending` 狀態。 最終，它可能會變成 `complete` 或 `cancelled`. 為確保您的Data Warehouse同步此變更，必須重新檢查欄中是否有新值。

這如何與 [復寫方法](../data-warehouse-mgr/cfg-replication-methods.md) 已經討論過了？ 重新檢查的處理方式會因所選的復寫方法而異。 此 `Modified\_At` 復寫方法是處理變更值的最佳選擇，因為不需要設定重新檢查。 此 `Auto-Incrementing Primary Key` 和 `Primary Key Batch Monitoring` 方法需要重新檢查設定。

使用其中一種方法時，必須標籤可變更的欄以重新檢查。 有三種方法可以達成此目的：

1. 作為要重新檢查的更新旗標欄的一部分執行的稽核程式。

   >[!NOTE]
   >
   >Auditor仰賴抽樣程式，因此可能不會立即擷取變更的欄。

1. 您可以自行設定，方法是選取Data Warehouse管理員中欄旁的核取方塊，然後按一下 **[!UICONTROL Set Recheck Frequency]**，並選擇適當的時間間隔，以檢查變更。

1. 成員隸屬於 [!DNL Adobe Commerce Intelligence] Data Warehouse團隊可以手動標籤欄，以便在您的Data Warehouse中重新入庫。 如果您知道可變更的欄，請聯絡團隊以請求設定重新檢查。 在您的要求中包含欄清單以及頻率。

## 重新檢查頻率 {#frequency}

**您知道嗎？**
設定重新檢查 `primary key` 欄不會檢查欄中是否有變更的值。 系統會檢查表格中是否有刪除的列，且會從Data Warehouse中清除任何刪除。

當欄被標籤為要重新檢查時，您也可以設定重新檢查發生的頻率。 如果特定欄不經常變更，則選擇不太頻繁的重新檢查可以 [最佳化您的更新週期](../../best-practices/reduce-update-cycle-time.md).

頻率選項包括：

* `always`  — 在每次更新期間進行重新檢查
* `daily`  — 重新檢查會在您宣告的時區的第一次午夜後更新時進行
* `weekly`  — 對於您宣告的時區，每星期晚上9點後都會進行重新檢查
* `monthly`  — 對於您宣告的時區，每四周於下午9點後重新檢查一次
* `once`  — 只會在下次更新時發生（一次性的重新整理）

由於更新時間與需要同步多少資料相關，Adobe建議選擇 `daily`， `weekly`，或 `monthly` 重新檢查而不是每次更新。

## 管理重新檢查頻率 {#manage}

按一下表格名稱，然後檢查個別欄，即可在Data Warehouse中管理重新檢查頻率。 同步狀態與重新檢查頻率( **變更？** 欄)會針對表格中的每個欄顯示。

若要變更重新檢查頻率，請按一下您要變更之欄旁的核取方塊。 然後按一下 **[!UICONTROL Set Recheck Frequency]** 下拉式清單並設定所需的頻率。

![](../../assets/dwm-recheck.png)

您有時可能會看到 `Paused` 在 `Changes?` 欄。 當表格的 [復寫方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 設為 `Paused`.

[!DNL Adobe] 建議檢閱這些欄，以最佳化更新並確保重新檢查可變更的欄。 如果根據資料變更的頻率，欄的重新檢查頻率很高，Adobe建議將其降低以最佳化更新。

如有疑問，請聯絡我們，或詢問目前的復寫方法或重新檢查。

**相關：**

* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
* [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
