---
title: 分段和篩選的建議資料Dimension
description: 瞭解細分和篩選的最佳實務。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# 細分和篩選

良好的細分可將膚淺的統計值轉變為推動決策的商業量度。

想知道您最有價值的客戶是誰？ 您最有價值的行銷管道為何？ 您的哪些產品進展更快？為什麼？ 若要取得上述任何答案，您必須先將資料分段。

本主題涵蓋經常向客戶建議的重要區段。 此外，也會詳細說明這些區段可協助您回答的問題。 技術上，區段是資料庫中的資料欄。 在 [!DNL Adobe Commerce Intelligence]，即維度。

![](../../mbi/assets/mbi-critical-segments.png)


## 使用者區段

使用者區段可協助您瞭解使用者的身分和行為。

* **年齡/出生年份**：您的使用者年齡為何？ 您最活躍的使用者年齡為何？ 通常將值分段到範圍中以便進行更有效的分析是有意義的。
* **性別**：不同性別與網站互動的方式是否不同？
* **地址**：您的使用者來自何處？ 您應該將行銷工作集中於特定地區嗎？ 您最近的廣告行銷活動是否如預期在目標地區執行？
* **客戶贏取來源**\：您知道使用者來自哪個行銷管道嗎？ 他們是否點按廣告或透過搜尋找到您？ [依使用者贏取來源將資料分段](../data-analyst/analysis/google-track-user-acq.md) 是最佳化新客戶贏取的第一步。 第二步是花更多錢在有效專案上，扼殺無效專案。
* **註冊裝置**：使用者是否透過您的行動應用程式或網站註冊？ iOS或Android™？ 您的行動使用者基礎是否足以配置更多資源來開發您的行動產品？ 如果您尚未追蹤此專案，請參閱此主題 [關於追蹤使用者裝置](../data-analyst/analysis/track-usr-dev-browser.md).
* **反向連結者**：誰是您影響最大的人？ 有多少位使用者被其他人直接引用？
* **產業**：如果您是B2B企業，您的使用者在哪些產業工作？ 哪些貿易組織值得加入？
* **調查回覆**：如果您執行客戶調查，請將回應作為區段使用，以進行更深入的分析。 您可以提出問題，以補充您已瞭解的使用者或確認您的猜測。
* **第一筆訂單金額與產品類別**：使用者的第一筆訂單與未來購買模式之間是否有相關性？

## 訂單/事件區段

訂單和事件區段可協助分析一段時間內的使用者行為和參與度。

* **[!UICONTROL Billing / Shipping Address]**：您的大多數訂單來自何處？ 帳單地址與送貨地址之間是否有差異？
* **[!UICONTROL Status]**：您有多少訂單無法完成？ 過去七天擱置訂單的比率是多少？
* **[!UICONTROL Customer acquisition source]**：除了在使用者層級追蹤使用者贏取資料外，您也可以 [在訂單或事件層級上追蹤](../data-analyst/analysis/google-track-user-acq.md). 透過一個來源註冊的使用者完全可以繼續透過其他來源存取您的網站。
* **[!UICONTROL Device]**：行動訂單數量增加嗎？ 您的收入中有多少是透過行動裝置購買產生的？ (如果您尚未追蹤此專案，請參閱本主題 [關於追蹤訂單裝置資料](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**：您的哪一個履行中心產生最多收入？ 如果您正在分析訂單時間與出貨時間之間的差異，哪一個履行中心的回應速度最快？
* **[!UICONTROL Delivery Carrier]**：哪一家是最受歡迎的電信業者？ 哪個承運商的退貨料號數量最少？
* **[!UICONTROL Discount / Coupon Codes]**：您的促銷活動是否真的帶來額外業務？ 除了待售的料號外，您的客戶還購買了多少額外料號？ 抵用券如何影響平均訂購值？ 折扣與非折扣專案的平均利潤是多少？
* **[!UICONTROL Satisfaction / Rating]**：客戶對訂單的滿意度為何？ 您的客戶可能會將業務轉介給您嗎？

## 產品區段

產品區段可協助您進行銷售決策。

* **[!UICONTROL Merchant / Brand]**：某個特定品牌的銷售速度是否比其他品牌快？ 哪些品牌表現缺佳？
* **[!UICONTROL Type / Category]**：不同的使用者區段會使用不同型別的產品嗎？ 哪些產品類別產生的重複業務最多？
* **[!UICONTROL Discount / Coupon Codes]**：促銷活動是否會影響非折扣產品的銷售？ 優惠券如何影響您產品的感知價值？
* **[!UICONTROL Social Activity]**：社群媒體產生的熱門話題與產品的銷售量之間是否有相關性？
* **[!UICONTROL Size / Variant]**：您需要每個變體的詳細目錄比率是多少？ 哪些變體可以折扣率出售？

如果您對銷售感興趣，請檢視 [如何使用產品區段推動業務重複](../data-analyst/analysis/most-value-source-channel.md).

## 建立客戶設定檔

細分專家可能想要超越一維切片，並開始建立真正的客戶個人檔案。 例如，年齡介於13至24歲之間且透過行動裝置註冊的人，會加入「Young &amp; Mobile」群組。 此群組的行為與您其他使用者群相比如何？

這類分析就是《財富》1000強公司行銷人員一整天的工作。 在雲端商務智慧平台(例如 [!DNL Commerce Intelligence]，這基本上是我們其他人無法企及的。 幸運的是，現在情況已完全不同。

## 追蹤新區段

依照上述維度來劃分量度的第一個步驟，就是確保您在資料庫中追蹤此資料。 如果未受到追蹤，請和您的技術團隊會面，並找到開始追蹤此資料的方法。

確認資料庫中已追蹤資料後， [聯絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 若要將維度推送至 [!DNL Commerce Intelligence] 度量和圖表。 您也可以使用 *欄位管理* 用於追蹤這些欄位的工具 [!DNL Commerce Intelligence].

## 相關

* [最佳化資料庫以進行分析](../best-practices/opt-db-analysis.md)
