---
title: Google Analytics中的UTM追蹤
description: 瞭解Google Analytics中UTM追蹤（標籤）的最佳實務。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM追蹤

`UTM` 追蹤是URL的標籤慣例，可讓您分析使用者的來源。 如果您檢視從大多數行銷電子郵件或橫幅廣告點按的URL，您會看到UTM標籤。 是那些長連結的結尾如下 `utm\_source` 和 `utm\_medium`.

[!DNL Google Analytics] 使用 `UTM` 標籤以瞭解流量的來源。 此資訊的部分來源為 [HTTP反向連結](https://en.wikipedia.org/wiki/HTTP_referer) 但其餘部分必須由您提供 `UTM` 引數。 當您看到 `google adwords` 或 `email marketing`，這表示 `UTM` 從原始連結點選記錄引數，然後儲存在使用者的Cookie中。 從那裡， [!DNL Google Analytics] 使用該資料來 [屬性有趣的行為](../data-analyst/analysis/google-track-user-acq.md) 在您的網站上。 瞭解這些引數的用途可協助您瞭解如何以最佳方式設定和使用UTM標籤。

## UTM標籤的最佳作法

以下列出設定您的URL時要記住的五個最重要事項 `UTM` 標籤。

### 1.目標是要標籤您可以控制的所有網站URL

每次您要求人員點按連結時，都應設定 `UTM` 標籤。 這包括您的所有電子郵件連結（您的電子郵件服務供應商可能會自動標籤您的URL）、廣告連結、新聞文章、部落格。

### 2.使用工具建立URL

`UTM` — 標籤的URL可能會很麻煩。 與其嘗試長時間鍵入它們，不如使用工具 [喜歡這個](https://support.google.com/analytics/answer/1033867?hl=en) 協助您。 這可確保您考慮將所有sensible引數新增至URL，並從URL中取得複製貼上的URL。 若要管理社交連結，可使用工具，如 [!DNL Hootsuite] 包含將自訂URL引數新增至所有連結的選項。

### 3.請確定引數值區分大小寫

請務必記住，標籤 `utm\_source=adwords` 是不同的標籤 `utm\_source=Adwords`. 請考慮讓所有內容都變成小寫。

### 4.將UTM引數值儲存在資料庫中

每次發生交易或事件時，您都要評估行銷活動的效能。 您可以讀取UTM引數值的值，從 [[!DNL Google Analytics] 將Cookie放入您的資料庫](../data-analyst/analysis/google-track-user-acq.md).

### 5.思考如何為行銷活動命名

為了追蹤您的行銷努力如何隨著時間改善，您需要對命名慣例有聰明的認識。 保持簡單，並儘可能最小化。 複雜的命名系統較難維護。

在資料庫中擷取此資料後，您可以透過更複雜的分析來評估行銷和廣告的效能，包括 [客戶期限值](../data-analyst/analysis/ess-expected-ltv.md)， [重複購買率](../data-analyst/analysis/repurchase-behavior.md)、和 [平均訂購值](../data-analyst/analysis/basic-analytics.md).
