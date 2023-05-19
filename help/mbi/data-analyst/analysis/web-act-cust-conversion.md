---
title: 分析網站活動和客戶轉換率
description: 瞭解如何設定儀表板來追蹤您的網站活動（包括頁面檢視、工作階段和使用者），以及您的客戶在一段時間內的轉換率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 分析網站活動

[!DNL Adobe Commerce Intelligence] 可讓您輕鬆將廣告成本資料與其餘資料整合。 這不僅可讓您瞭解您的網站活動，而且可讓您推匯出網站上成為註冊使用者或進行購買的訪客百分比。

此主題示範如何設定控制面板，追蹤網站活動（包括頁面檢視、工作階段和使用者）以及客戶在一段時間內的轉換率。

## 必要條件

**匯入您的廣告成本資料**  — 連線 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) 至 [!DNL Adobe Commerce Intelligence]  — 這會自動同步您的 [!DNL AdWords] Commerce Intelligence支出。

**追蹤使用者贏取管道資料**  — 繫結您的 [!DNL Google AdWords] 將資料與資料庫中的特定訂單對應，您必須 [追蹤使用者贏取](../analysis/google-track-user-acq.md) 透過 [!DNL Google Analytics E-commerce]. 這可讓您使用utm來源和媒體來連線每個訂單。

## 使用者贏取行銷活動

這份報表的集合是以下列方式建置：

* 連線時自動產生的量度 [!DNL Google AdWords] 資料
* 您的帳戶中應已可用的基本量度，例如 `Number of orders` 和 `New users`
* 加入時建立的Dimension [!DNL Google Analytics Ecommerce] 資料至您的資料庫，例如訂單的utm來源與訂單的utm媒體。 如果您的帳戶目前沒有這些欄位，請聯絡支援團隊

## 建立報告

**首先，建立顯示一段時間內頁面檢視、工作階段和使用者數量的報告：**

1. 建立報表。
1. 按一下 **[!UICONTROL Add Metric]**，然後將滑鼠移至 [!DNL Google Analytics] 區段並選取 `Page Views`.
1. 新增另一個量度，再次繫結在 [!DNL Google Analytics] 區段，這次選取 `Sessions`.
1. 新增第三個量度，再次繫結在 [!DNL Google Analytics] 區段，這次選取 `Users`.
1. 現在將您的時段變更為移動範圍（從31天前到1天前），並將時間間隔調整為 `by day`.
1. 為您的報表命名(例如， `Page views, sessions and users by day`)，然後按一下 **[!UICONTROL Save]**.

**第二個報表會檢視過去一年中的頁面檢視次數：**

1. 建立報表。
1. 按一下 **[!UICONTROL Add Metric]**，將游標移至 [!DNL Google Analytics] 區段並選取 _頁面檢視_.
1. 將您的時段變更為移動範圍（從13個月前到1個月前），並將時間間隔調整為 `by month`.
1. 為您的報表命名，例如 `Page views by month,` 並按一下 **[!UICONTROL Save]**.

**第三張圖表檢視過去一年的反彈率：**

1. 建立報表。
1. 按一下 **[!UICONTROL Add Metric]**，將游標移至 [!DNL Google Analytics] 區段並選取 _跳出率_.
1. 將您的時段變更為移動範圍（從13個月前到1個月前），並將時間間隔調整為 `by month`.
1. 為您的報表命名，例如 `Bounce rate by month`，然後按一下 **[!UICONTROL Save]**.

**現在，比較新訪客與回訪訪客的平均工作階段長度：**

1. 建立報表。
1. 按一下 **UICONTROL新增量度**，將游標移至 [!DNL Google Analytics] 區段並選取 `Average Session Length`.
1. 將您的時段變更為移動範圍（從13個月前到1個月前），並將時間間隔調整為 `by month`？
1. 新增 `Group by` 並選取 `New or returning visitor`.  檢查 `Show All` 方塊；然後按一下 **[!UICONTROL Apply]**.
1. 為您的報表命名，例如 `Average session length`，然後按一下 **[!UICONTROL Save]**.

**接下來，檢視過去30天內排名最前的反向連結網域：**

1. 建立報表。
1. 按一下 **[!UICONTROL Add Metric]**，將游標移至 [!DNL Google Analytics] 區段並選取 `Sessions`.
1. 將您的時段變更為移動範圍（從31天前到1天前），並將時間間隔調整為 `none`.
1. 新增 `Group by` 並選取 `ga:source`.  檢查 _全部顯示_ 方塊；然後按一下 **[!UICONTROL Apply]**.
1. 新增另一個 `group by` 並選取 `ga:medium`. 再次檢查 `Show All` 方塊；然後按一下 **[!UICONTROL Apply]**.
1. 為您的報表命名，例如 `Top 20 Referring Domains, 30 Days`，然後按一下 **[!UICONTROL Save]**.

**最後，檢視轉換：**

1. 建立報表。
1. 新增下列量度：

* `New users`
   * 按一下 **[!UICONTROL Hide]** 在量度名稱下方

* `Number of orders`
   * 新增篩選器 `Customer's order number` = 1並按一下 **[!UICONTROL Apply]**
   * 按一下量度名稱並呼叫它，以重新命名量度 `Number of first orders`，然後按一下 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 量度

* `Users`
   * **[!UICONTROL Hide]** 量度
   * 將時段變更為 `24 months ago to now`，並將時間間隔調整為 `by month`.
   * 按一下「 」，新增下列公式 **[!UICONTROL Formula]**.
   * A/D，然後按一下 **[!UICONTROL Apply]**
   * 重新命名公式 `Registration conversion`
   * B/D ，然後按一下 **[!UICONTROL Apply]**
   * 重新命名公式 `First order conversion`
   * C/D，然後按一下 **[!UICONTROL Apply]**
   * 重新命名公式 `Any order conversion`

* 現在為您的報表命名，例如 `Conversion by month`，然後按一下 **[!UICONTROL Save]**.

## 後續步驟

現在您可以存取有關您網站流量和轉換率的資料，您可以開始發掘這些資料以推動業務決策，例如哪些網站最能帶來您網站的流量？ 或您的哪些行銷活動最能有效吸引具有高期限價值的客戶？

當您調整廣告支出和行銷策略時，可以繼續追蹤以下專案的成效： [!DNL Commerce Intelligence]，在此控制面板上反複處理，以符合貴公司不斷變化的優先順序。
