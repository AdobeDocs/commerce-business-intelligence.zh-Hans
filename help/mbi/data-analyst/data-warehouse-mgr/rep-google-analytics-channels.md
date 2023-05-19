---
title: 使用贏取來源複製Google Analytics管道
description: 瞭解如何使用贏取來源來復寫Google Analytics管道。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] 使用贏取來源

## 什麼是管道？ {#channels}

建立自訂區段來檢視不同流量的表現和觀察趨勢，是對最強大的用途之一 [!DNL Google Analytics]. 預設存在於中的一個區段類別 [!DNL Google Analytics] 是 `Channels`. 管道是使用者造訪您網站的一組常見方式。  [!DNL Google Analytics] 自動排序您取得使用者的許多方式（無論是社群媒體、每次點按付費、電子郵件或轉介連結），並將其整合到貯體或頻道中。

## 為什麼我看不到我的 `channels` （在Commerce Intelligence？） {#nochannels}

`Channels` 是簡單的彙總資料貯體。 若要將您的贏取排序至管道值區， [!DNL Google] 使用特定引數設定不同的規則和定義：贏取組合 [來源](https://support.google.com/analytics/answer/1033173?hl=en) （流量的來源）和贏取 [中](https://support.google.com/analytics/answer/6099206?hl=en) （來源的一般類別）。

雖然擁有這些貯體可協助您瞭解流量的來源，但此資料不會透過管道進行標籤，而是透過來源和中介的組合進行標籤。 因為 [!DNL Google] 以兩個個別的資料點傳送管道資訊，管道分組不會自動顯示於 [!DNL Commerce Intelligence].

## 什麼是預設的管道群組？ 它們是如何建立的？

依預設， [!DNL Google] 設定八個不同的管道。 決定如何建立管道的規則如下。

| **頻道** | **這是什麼？** | **它是如何建立的？** |
|---|---|---|
| 直接 | 直接進入您網站的人。 | 來源= `Direct`<br>AND中= `(not set); OR Medium = (none)` |
| 有機搜尋 | 已有機地在無償搜尋引擎中排名的流量。 | 中= `organic` |
| 轉介 | 來自非有機搜尋外部連結或非社交網路網站的流量。 | 中= `referral` |
| 付費搜尋 | 具有UTM追蹤程式碼的流量，其中媒體為「cpc」、「ppc」或「paidsearch」，並且是不符合「內容」的廣告散佈網路。 | 中= `^(cpc|ppc|paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| 社交 | 反向連結流量來自以下任何一項：大約 [400個社交網路](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 和不會被標籤為廣告。 | 社交來源轉介= `Yes`<br>或中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子郵件 | 來自使用「電子郵件」媒介標籤的工作階段的流量。 | 媒體的UTM追蹤代碼= `email` |
| 顯示 | 具有UTM追蹤程式碼（媒體為顯示或cpm）的流量。 也包括廣告散佈網路符合「內容」的AdWords互動 | 中= `^(display|cpm|banner)$`<br>OR廣告散佈網路= `Content`<br>AND廣告格式≠ `Text` |
| 其他 | 其他廣告頻道（不包括付費搜尋）的工作階段，並以&quot;cpc&quot;、&quot;ppc&quot;、&quot;cpm、&quot;cpv&quot;、&quot;cpa&quot;、&quot;cpp&quot;、&quot;affiliate&quot;等媒體標籤。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## 如何在Data Warehouse中重新建立這些管道群組？ {#recreate}

現在您知道管道只是來源和媒體的組合，在Data Warehouse中重新建立這些分組是簡單的3步驟流程。

1. **啟用您的[!DNL Google ECommerce]整合**

   [啟用時](../importing-data/integrations/google-ecommerce.md)，請確定 [同步](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **中** 和 **source** Data Warehouse中的欄位。 完成此作業後，媒體與來源贏取資料將會帶入您的Data Warehouse。

1. **上傳Google的管道分組對應**

   Adobe Commerce會建立表格，並將預設群組對應為檔案，您可以 [下載](../../assets/ga-channel-mapping.csv).

   如果您是 [!DNL Google Analytics] pro並建立您自己的管道，您想要先將特定規則新增至對應表格，然後再將檔案上傳至 [!DNL Commerce Intelligence].

   將其帶入您的Data Warehouse，作為 [檔案上傳](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **建立以下專案之間的關係：[!DNL Google ECommerce]和對應檔案上傳**

   若要建立[!DNL Google ECommerce] 和對應表， [提交支援要求](../../guide-overview.md#Submitting-a-Support-Ticket) 至您的資料分析團隊並參考此主題。 分析人員會建立新的計算欄，稱為 **頻道** 在電子商務表格中。 **在完整更新週期後**，此欄將可在 `Filter` 或 `Group by`.

您現在擁有 [!DNL Google Analytics Channel] Data Warehouse中的分組，這表示您可以從新的角度分析資料：

![依管道將「訂單數」量度分段](../../assets/GA_Channel_Gif.gif)

在此範例中，您一開始是透過分段 **訂單數** 量度依據 **頻道**. 測試新欄，看看您可在中識別哪些趨勢 [!DNL Google Analytics Channel] 資料！

## 相關檔案

* [使用Report Builder](../../tutorials/using-visual-report-builder.md)
* [預期[!DNL Google ECommerce]資料](../importing-data/integrations/google-ecommerce-data.md)
* [建置[!DNL Google ECommerce]包含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [您最寶貴的贏取來源和管道為何？](../analysis/most-value-source-channel.md)
