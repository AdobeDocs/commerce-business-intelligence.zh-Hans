---
title: Google Analytics — 追蹤使用者贏取來源資料概述
description: 瞭解如何依使用者贏取來源劃分資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: af1e3839839b4c419beabb0cc666c996ea2179d4
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# 依使用者贏取來源細分

>[!NOTE]
>
>以下程式不支援 [!DNL Google Universal Analytics].

依使用者贏取來源劃分資料區段的能力是有效管理行銷計畫的關鍵。 瞭解新使用者的贏取來源，可顯示哪些管道產生最高回報，並讓您的團隊充滿信心地配置行銷資金。

如果您尚未追蹤資料庫中的使用者贏取來源， [!DNL Adobe Commerce Intelligence] 可以協助您開始使用：

## 追蹤使用者贏取來源

[!DNL Adobe] 建議根據您的設定使用兩種方法追蹤反向連結來源資料：

### （選項1）透過以下方式追蹤訂單轉介來源資料： [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您使用 [!DNL Google Analytics E-Commerce] 若要追蹤您的訂單與銷售資料，您可以使用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 以同步每個訂單的轉介來源資料。 這可讓您依反向連結來源來劃分收入與訂單(例如， `utm_source` 或 `utm_medium`)。 您也可以透過以下方式瞭解客戶贏取來源 [!DNL Commerce Intelligence] 自訂維度，例如 `User's first order source`.

>[!NOTE]
>
>**適用於Shopify使用者**：開啟 [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) 在連線您的 [!DNL Google Analytics E-Commerce] 帳戶至 [!DNL Commerce Intelligence].

### （選項2）儲存 [!DNL Google Analytics]&#39;資料庫中的贏取來源資料

本主題說明如何儲存 [!DNL Google Analytics] 贏取管道資訊放入您自己的資料庫，即 `source`， `medium`， `term`， `content`， `campaign`、和 `gclid` 使用者第一次造訪您的網站時顯示的引數。 如需這些引數的說明，請檢視 [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 然後，您會探索可使用此資訊在中執行的一些強大行銷分析 [!DNL Commerce Intelligence].

#### 為什麼？

如果您只檢視預設值 [!DNL Google Analytics] 轉換和贏取量度，你就無法掌握全貌。 雖然檢視有機搜尋與付費搜尋的轉換次數很有趣，您可以如何處理這些資訊？ 您應該在付費搜尋上花更多錢嗎？ 這取決於來自該管道的客戶的價值，這不是Google Analytics提供的東西。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 透過將交易資料儲存在中來緩解此問題 [!DNL Google Analytics]，但此解決方案不適用於非電子商務網站。 此外，某些工具（例如同類群組分析）在中不易執行， [!DNL Google Analytics] 介面。

如果您想要透過電子郵件向所有從特定電子郵件促銷活動取得的客戶傳送後續交易，該怎麼做？ 或是將贏取資料與CRM系統整合？ 這是不可能的 [!DNL Google Analytics]  — 事實上，這違反了 [!DNL Google Analytics] 儲存可識別個人的任何資料。 不過，您可以自行儲存此資料。

#### 方法

[!DNL Google Analytics] 會將訪客反向連結資訊儲存在名為的Cookie中 `__utmz`. 在此Cookie設定後(由 [!DNL Google Analytics] 追蹤程式碼)，其內容將會隨著該使用者的每次後續請求傳送至您的網域。 因此，例如，在PHP中，您可以將 `$_COOKIE['__utmz']` 而且您會看到類似以下的字串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

很明顯有一些贏取來源資料會編碼為字串。 測試以確認這是訪客的最新贏取來源和相關聯的行銷活動資料。 現在您需要瞭解如何擷取資料。

此程式碼已轉譯為 [在github上託管的PHP程式庫](https://github.com/RJMetrics/referral-grabber-php). 若要使用程式庫， `include` 參考 `ReferralGrabber.php` 然後呼叫

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

傳回的 `$data` 陣列是索引鍵的對應 `source`， `medium`， `term`， `content`， `campaign`， `gclid`，以及各自的值。

[!DNL Adobe] 建議將名為的表格新增至資料庫，例如 `user_referral`，具有以下欄： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每當使用者註冊時，請擷取反向連結資訊並將其儲存至此表格。

#### 如何使用此資料

現在您正在儲存使用者贏取來源，該如何使用？

假設您正在使用SQL資料庫，而且具有 `users` 表格具有下列結構：

| ID | 電子郵件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有機 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 轉介 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有機 |
| ... | ... | ... | ... | ... |

首先，您可以對資料庫執行下列查詢，以計算來自每個轉介管道的使用者數量：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果如下所示：

| ACQ_SOURCE | 使用者計數 |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 轉介 | 55 |
| 其他 | 16 |

這很有趣，但用途有限。 您真正想瞭解的是：

* 這些數字在一段時間內的成長率
* 每個贏取來源產生的收入金額
* a [同類群組分析](https://en.wikipedia.org/wiki/Cohort_analysis) 來自每個來源的使用者數量
* 這些管道之一的使用者未來會以客戶身分回訪的可能性。

執行這些分析所需的查詢很複雜。 有了這些資訊，您就可以決定獲利最多的贏取管道，並相應地集中行銷時間和金錢。

### 相關

* **[探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)**
* **[連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM歸因是否有效？](../analysis/utm-attributes.md)**
