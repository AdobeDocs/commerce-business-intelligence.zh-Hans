---
title: 在視覺Report Builder中使用時間選項
description: 瞭解如何分析特定時段內的報表資料。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# 使用 [!DNL Time] 中的選項 [!DNL Visual Report Builder]

功能之一 [!DNL Visual Report Builder] 是全域 `Time Range` 和 `Interval` 設定。 這些設定可讓您分析特定時段內的報表資料。

不過，對於某些分析，您可能需要在同一報告中考慮不同的「時間範圍」或「時間間隔」。 這就是 `Time` 有選項可用。 讓您更清楚瞭解如何使用 `Time` 選項的相關資訊，本教學課程涵蓋下列使用案例：

* [分析沒有時間戳記的量度](#notimestamp)
* [指定一個量度獨立的時間間隔](#independenttimeinterval)
* [比較不同時間範圍內的相同量度](#difftimerange)

如果您想要遵循本主題中討論的一些範例報告，請開啟 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) 然後再繼續。

## 分析沒有時間戳記的量度 {#notimestamp}

有些量度無法隨著時間推移而改變，因為資料並未收集或與相關聯的時間戳記一起儲存。 例如，詳細目錄表格通常只包含每個SKU的一列。 在這種情況下，您應： [建立量度](../data-user/reports/ess-manage-data-metrics.md) 而不指定時間戳記。

在報表中使用此類量度時，您會注意到將此量度新增至報表會自動設定獨立的 `Time Interval` 之 `None` 和 `Time Range` 之 `Global`：

![](../assets/Metrics_without_timestamps.gif)

## 指定一個量度獨立的時間間隔 {#independenttimeinterval}

`Time` 選項可讓您建立以時間為基礎的100%圖表，以識別在特定時間範圍內哪一天、周、月或年貢獻了最大的值。 在此區段中，您會建立圖表來顯示一年中每個日曆月所產生的收入百分比。

如果您想要比較逐年產生的收入，這類報表就十分實用。 舉例來說，您有一張2015年的圖表顯示，1月貢獻了該年度18%的收入，而另一張2016年的圖表只顯示8%。 您可以開始研究可能已發生的情況。

1. 新增您的 `Revenue` 報表的量度。
1. 按一下 **[!UICONTROL Duplicate]** 製作量度的副本。
1. 按一下全域 **[!UICONTROL Time Range]** 選項，然後 **[!UICONTROL Moving Time Range]**. 將此專案設為 `Last Year`.
1. 按一下全域 **[!UICONTROL Time Interval]** 選項並將其設定為 `Monthly`.
1. Report Builder會自動為第二個量度新增第二個Y軸。 取消選取 `Multiple Y-Axes` 方塊。
1. 接下來，您套用獨立的 `Time Interval` 至第一個量度。 按一下 **[!UICONTROL Time Options]** （時鐘圖示） `first Revenue metric`.
1. 按一下 **[!UICONTROL Time Options]** 在報表上方顯示的展開視窗中。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此項設為 `None`.

   * `Time Range`：將此項設為 `Last Year` 按一下 **[!UICONTROL Custom]**，則 **[!UICONTROL Moving Range]**，最後選取 `Last Year` 選項。

   * 按一下 **[!UICONTROL Apply]** 以儲存間隔和範圍設定。 這會建立一個量度，用於計算上一年度的總收入。 接下來，您將此量度當作公式中的分母。

   * 若要檢視每個月的收入百分比，您必須將公式新增至報表。 按一下 **[!UICONTROL Add Formula]**.

   * 輸入 `B/A` 在公式欄位中並選取 `% Percent` 文字欄位旁的下拉式清單。 此公式將去年特定月份的收入金額除以去年的收入總額。

   * 按一下 **[!UICONTROL Apply Changes]**.

   * 隱藏兩個輸入量度並重新命名公式。

現在您可以瞭解去年每個月的影響力有多大：

![](../assets/Independent_Time_Int.png)

## 比較不同時間範圍內的相同量度 {#difftimerange}

此範例使用自訂維度，稱為 `Day number of the month`. 如果您想要建立此報表，但您的Data Warehouse中還沒有此維度， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以取得協助。

此類別中最常見的兩個範例是(1)比較成長量度（收入逐年比較或逐月比較），以及(2)更瞭解最近的存貨或料號銷售趨勢。

若要示範此使用案例，請檢視上個月的每日收入與去年同期比較。 假設您想檢視2016年1月的每日收入，然後與2015年1月、2014年1月等比較，此報表會顯示該情形。

1. 新增您的 `Revenue` 報表的量度。
1. 按一下 **[!UICONTROL Duplicate]** 製作量度的副本。
1. 將第一個量度重新命名為 `Items sold last 7 days` 第二個量度至 `Items sold last 28 days`.
1. 按一下 **[!UICONTROL Time Range]**，則 **[!UICONTROL Moving Time Range]**. 將此專案設為 `Last Month`.
1. 按一下 **[!UICONTROL Time Interval]** 並將其設定為 `None`.
1. 按一下 **[!UICONTROL Time Options]** （時鐘圖示） `Revenue` 量度。
1. 按一下 **[!UICONTROL Time Options]** 在報表上方顯示的展開視窗中。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此項設為 `None`.

   * `Time Range`：將此項設為 `From 14 Months Ago To 13 Months Ago` 按一下 **[!UICONTROL Custom]** 則 **[!UICONTROL Moving Range]**. 使用功能表頂端的欄位和下拉式清單來設定範圍。 此設定可讓我們檢視上個月的收入，但同時也是上一年度的收入。
   如果量度從報表中消失，不必擔心，設定獨立時間選項會自動隱藏報表中的量度。 若要重新顯示，請按一下 **[!UICONTROL Show]** 量度旁邊。

   ![](../assets/Different_Time_Ranges.gif)

   * 按一下 **[!UICONTROL Apply]** 以儲存間隔和範圍設定。

   * 接下來，您新增自訂 `Day number of the month` 按一下以建立維度 **[!UICONTROL Group By]** 並選取維度。 這會傳回訂單當月的日期編號，例如，3月2日下單的訂單會傳回 `2`.

   * 在 `Group By` 下拉式清單，選取 `Show All` 並按一下 **[!UICONTROL Apply]**. 這會建立報表的X軸值：

   ![](../assets/TO4.png)

   * 重新命名量度。 在此範例中，第一個量度是 `Revenue - 2015` 第二個是 `Revenue - 2014`.



自訂的另一個常見用法 `Time Options` 是決定供應的周數。 特別是在節日季節或特殊促銷期間，您可能想要考量過去一週、一個月和上一個促銷期間所出售的料號，以做出明智的購買決定。

請記得在自行建立此報表時，將時間範圍設定為您所需的設定。

1. 新增您的 `Items Sold` 報表的量度。
1. 按一下 **[!UICONTROL Duplicate]** 製作量度的副本。
1. 重新命名量度。 您可以使用相同的名稱或類似名稱：
   1. 將第一個量度重新命名為 `Items sold last 7 days`.
   1. 將第二個量度重新命名為 `Items sold last 28 days`.
1. 於 `Items sold last 7 days` 量度，按一下全域 **[!UICONTROL Time Range]** option then **[!UICONTROL Moving Time Range]**. 在此範例中，您將其設為 `Last 7 Days`.
1. 按一下 **[!UICONTROL Time Interval]** 並將其設定為 `None`.
1. 接下來，您定義 `Time Options` 的 `Items sold last 28 days` 量度。 按一下 **[!UICONTROL Time Options]** （時鐘圖示） `second Items sold` 量度。
1. 按一下 **[!UICONTROL Time Options]** 在報表上方顯示的展開視窗中。
1. 在下拉式清單中，設定下列專案：

   * `Time Interval`：將此項設為 `None`.
   * `Time Range`：將此項設為 `From 29 days to 1 day ago` 按一下 **[!UICONTROL Custom]**，則 **[!UICONTROL Moving Range]**. 使用功能表頂端的欄位和下拉式清單來設定範圍。
   * 按一下 **[!UICONTROL Apply]** 以儲存間隔和範圍設定。
   * 複製 `Items sold last 28 days` 量度並開啟新量度的 `Time Options`. 設定下列選項：

      * `Time Interval`：將此項保留為 `None`.
      * `Time Range`：按一下「 」，將此變更為符合您感興趣之促銷活動的日期範圍 **[!UICONTROL Specific Date Range]** 然後輸入適當的日期。
      * 重新命名量度 `Items sold during last promotion` 或類似專案。
      * 新增您的 `Units on hand` 量度。
      * 接下來，您必須新增計算值，顯示時間期間的庫存周數（考慮銷售趨勢）(`last 7 days`， `last 28 days`、和 `last promo` 期間)，您會將包含在報表中。 您必須為每個時段執行此操作一次。

若要建立公式，請按一下 **[!UICONTROL Add Formula]**. 在下方輸入公式，然後按一下 **[!UICONTROL Apply Changes]** 完成後。 對三個時段中的每個時段重複此步驟：

* 對於 `last 7 days time period`，輸入 `D / A` 在 `Formula` 欄位。
* 對於 `last 28 days time period`，輸入 `D / (B/4)` 在 `Formula` 欄位。

   >[!NOTE]
   >
   >請務必在此標準化您所選取的時間範圍。 在此範例中，將28天分成四周。 您可能需要將不同的邏輯套用至公式。

* 對於 `last promo period`，輸入 `D / C` 在 `Formula` 欄位。

   ![](../assets/Different_Time_Ranges_2.png)

* 最後，隱藏量度並新增「 」來自訂報表 `SKU` 或與報表類似的維度 `Group By`.

此範例說明目前的存貨層次適合全產品14天銷售。 不過，新增可比較的促銷期間時，表示公司需要進行一些變更，要麼訂購更多存貨，要麼只促銷庫存量足夠的料號。

由於客戶在一段時間內的行為不同，執行分析時，您可能會看到資料中的差異。 設定自訂時間選項可讓您快速建立複雜的分析，啟用將歷史趨勢納入考量的資料導向式決策。

