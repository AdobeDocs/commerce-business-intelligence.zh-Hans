---
title: Google Analytics和UTM歸因
description: 瞭解Google Analytics來源歸因程式。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] 和UTM歸因

關鍵在於 [追蹤使用者贏取來源](../../data-analyst/analysis/google-track-user-acq.md) 至 [識別績效最佳的廣告行銷活動](../../data-analyst/analysis/most-value-source-channel.md). 本主題探討 [!DNL Google Analytics] 來源歸因程式。 換句話說，會在何時記錄哪一條資訊。

## 什麼是歸因？

`Attribution` 是關於指定特定活動的轉介來源。 這些活動通常是巨集轉換或微集轉換，巨集是類似以下的專案 **購買**，微型 **註冊、電子郵件註冊、部落格評論、** 等等。

理想情況下，每當發生轉換事件時，就會記錄反向連結來源。 但如何判斷來源？

現實情況是，使用者在點選/認可微或巨集轉換之前，通常來自許多來源。 例如，他們可能透過有機方式造訪網站，然後離開，接著透過付費搜尋造訪，然後離開，然後直接造訪網站本身。 此來源追蹤資訊通常透過UTM引數提供給網站，但也有更複雜的系統。 基於您的目的，專注於 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 如何 [!DNL Google Analytics] 是否透過UTM引數來屬性轉介來源？

在URL上指定UTM引數時，這些引數會經過剖析並放入 [!DNL Google Analytics] [Cookie](https://en.wikipedia.org/wiki/HTTP_cookie). 如果網站沒有 [!DNL Google Analytics]，擁有UTM沒有任何意義。 [!DNL Google Analytics] 有關於如何處理在其存留期內使用UTM點選多個URL之使用者的規則（稍後將詳加說明）。 假設網站已設定為將UTM引數擷取至外部資料庫，則當微或巨集轉換發生時，無論何處 [!DNL Google Analytics] 轉換時的Cookie會複製到資料庫。

## 首次點按與上次點按

### 最後點按歸因

最後點按歸因是使用者最常使用的歸因模型。 [!DNL Google Analytics]. 在此案例中， [!DNL Google Analytics] Cookie代表轉換事件前最新來源的UTM引數，這為 [記錄在資料庫中](../../data-analyst/analysis/google-track-user-acq.md). 此 [!DNL Google Analytics] 只有當使用者點按包含一組新UTM引數的新URL時，Cookie才會覆寫先前的UTM引數。

例如，假設使用者是透過第一次造訪網站 [!DNL Google Analytics] *付費搜尋*，然後傳回： *有機搜尋*，最後返回 *直接網站* 或透過 *電子郵件連結* **不含UTM引數** 轉換事件之前。 在此範例中， [!DNL Google Analytics] Cookie指出使用者的來源是有機的，因為這代表轉換前的最後一個來源。 此 *路徑* 忽略該最終轉換事件之前的ID。 如果使用者改為透過具有UTM的電子郵件連結造訪網站，則 [!DNL Google Analytics] Cookie會指出來源為「電子郵件」。 因此，如果Cookie中存在現有的UTM引數，且使用者透過直接進入，則 [!DNL Google Analytics] Cookie會顯示UTM引數，而非「直接」。

>[!NOTE]
>
>特定使用者的 [!DNL Google Analytics] Cookie引數會在Cookie時清除 [過期](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)，或使用者在瀏覽器中清除其Cookie時。*

### 首次點按歸因

有些付費歸因工具可讓您在使用者路徑中擷取來源的「煎餅棧疊」。 在這種情況下，在上述範例中，首次點按歸因將會告訴我們付費搜尋。 或者，有些網站會實作自己的Cookie，擷取煎餅棧疊，並將第一個來源儲存至其資料庫。

## 如何分析歸因？

[!DNL Google Analytics] 在其Web介面中具有一些強大的功能，可讓您執行四種不同的歸因模型：

1. 首次點按
1. 最後點按
1. 線性（將收入平均分配到路徑中的所有來源）
1. 加權（自訂歸因）

現在您瞭解每個微轉換或巨集轉換的歸因模型後，問題變成「您如何處理使用者的所有轉換？」。  例如，檢視根據GA上次點按邏輯記錄的UTM：

* 使用者在有機底下註冊
* 使用者在付費搜尋下的首次購買$5.00
* 使用者在電子郵件$50.00下的第二次購買
* 使用者第三次購買有機費$10.00

您會在這裡問：「我從付費搜尋獲得多少收入？ 來自電子郵件？  有機食品？」。 您可以說答案是5、50和10 （無論最後一個來源為何），或者您也可以說將所有收入歸因於第一個來源（所有65個都歸因於有機來源）。 您也可以套用一些加權分析或套用線性模型（即每個模型大約22個）。

## 相關檔案

* [透過以下方式追蹤訂單反向連結來源： [!DNL Google Analytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../analysis/google-track-user-acq.md)
* [追蹤資料庫中的使用者裝置、瀏覽器和作業系統資料](../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)
* [在中進行UTM標籤的五個最佳做法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
