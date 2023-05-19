---
title: 識別您最有價值的行銷資源和管道
description: 瞭解可用來揭露您最有價值行銷管道的一些報告。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 識別成功的行銷來源

您調查了對象、建立了行銷活動、投資了幾個行銷管道。 一段時間過去了，這些管道的表現如何？ 哪個頻道吸引的新使用者最多？ 哪一個來源對您的總收入貢獻最大？

替換為 [!DNL Adobe Commerce Intelligence]，您可以依反向連結來源輕鬆劃分收入和使用者，無論其是否符合 [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) 或自訂資料欄位。 此細分可讓您找到績效最佳的管道，並更好地投入行銷預算。

本主題探索可用來發掘您最有價值行銷管道的一些報告：

* [依來源的新使用者](#newusersbysource)
* [依使用者來源的平均期限收入](#avglifetimerev)
* [依使用者來源的平均訂單值](#avgorderval)
* [依使用者註冊日期和來源列出的收入](#revbyregdateandsource)
* [依使用者來源重複訂單](#repeatordersbysource)

## 必要條件 {#prereqs}

若要建立本主題中的分析，您需要存取行銷贏取/轉介來源資料。 如果您尚未進行追蹤，則需要 [訂單反向連結來源資料來源 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) 到 [!DNL Adobe Commerce Intelligence] 才能繼續。 此外，將使用者裝置資訊新增至分析時，可讓您檢視反向連結所使用的技術。

## 依來源的新使用者 {#newusersbysource}

評估反向連結來源的效能是決定您最有價值管道的關鍵。 此報表會依贏取來源顯示一段時間內新註冊的使用者數量，讓您在贏取新註冊使用者時可追蹤轉介來源的效能。

若要在中建立此報告 [Report Builder](../../tutorials/using-visual-report-builder.md)，新增 **新使用者** 報表中的量度（或計算一段時間內新使用者人數的同等量度）。 然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的註冊期間。
1. 設定 [!UICONTROL Interval] 至每月。
1. 設定 [!UICONTROL Group By] 至贏取（或轉介）來源，並選取您要包含的來源。
1. 此範例使用 `stacked columns` [!UICONTROL chart type].

以下是視覺化逐步解說：

![建立依來源的新使用者報表。](../../assets/New_Users_by_source.gif)

## 依使用者來源的平均期限收入 {#avglifetimerev}

尋找帶來新使用者的管道很重要，但這些反向連結整體上有多大價值？ 此報表顯示一段時間內，來自特定贏取來源的使用者平均期限收入。 換言之，這可讓您檢視從特定來源取得的使用者在其一生中與您共用的時間是否比從不同來源取得的一組使用者多。

若要在Report Builder中建立此報表，請新增 **平均期限收入** 報表的量度。 然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的時段。
1. 設定 [!UICONTROL Interval] 至每月。
   [!UICONTROL Group By] 至贏取（或轉介）來源，並選取您要包含的來源。
1. 此範例使用 `line chart` 型別。

以下是視覺化逐步解說：

![依使用者來源建立平均期限收入](../../assets/Lifetime_revenue_by_user_source.gif).

此範例只會檢視期限收入，但您也可以復寫此分析，以檢視 [!UICONTROL Number of orders] 或 [!UICONTROL Distinct buyers] 依反向連結來源。

## 依使用者來源的平均訂單值 {#avgorderval}

若要更清楚瞭解使用者從特定贏取來源花費了多少錢，您可以建立報表來檢視其平均訂單值。 這可讓您追蹤從特定來源取得的使用者在每一訂單上的花費是否比從其他來源取得的使用者多。

若要在Report Builder中建立此報表，請新增 **平均訂購值** 量度，然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的註冊期間。
1. 設定 [!UICONTROL Time Interval] 至每月。
1. 設定 [!UICONTROL Group By] 至贏取（或轉介）來源，並選取您要包含的來源。
1. 此範例使用 **棧疊欄** 圖表型別。

以下是視覺化逐步解說：

![建立依使用者來源的平均訂單值報表。](../../assets/Average_order_value_by_source.gif)

## 依使用者註冊日期和來源的總收入 {#revbyregdateandsource}

先前涵蓋的期限收入分析可讓您檢視從不同來源取得的使用者平均期限收入，但期限收入總計呢？ 此報表可讓您識別在特定時間內註冊並從特定來源產生多少整體收入。

若要在Report Builder中建立此報表，請新增 `Revenue by user registration date` 量度。 如果您沒有 [已建立此量度](../../data-user/reports/ess-manage-data-metrics.md) 您已經可以複製 `Revenue` 量度與變更 `time stamp` 至使用者的 `creation date`. 新增量度後，請執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的註冊期間。
1. 設定 [!UICONTROL Time Interval] 至每月。
1. 設定 [!UICONTROL Group By] 至贏取（或轉介）來源，並選取您要包含的來源。
1. 此範例使用 `stacked columns` 圖表型別。

以下是視覺化逐步解說：

![建立依使用者註冊日期和來源的總收入報表。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 依使用者來源重複訂單 {#repeatordersbysource}

「平均訂單值」報表平均會顯示從特定來源取得的使用者在下訂單時花費的金額。 但是，此報表不會顯示這些相同的使用者是否為回頭客戶。 但透過使用者來源的重複訂單，您可以檢視特定來源的使用者是否進行更多或更少的重複購買。

若要在中建立此報告 [Report Builder](../../tutorials/using-visual-report-builder.md)，新增 **訂單數** 量度，然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的註冊期間。
1. 設定 [!UICONTROL Time Interval] 至每月。
1. 新增 [!UICONTROL filter] 以便只包含具有重複訂單的使用者：

   使用者訂單編號大於1

1. 設定 [!UICONTROL Group By] 至贏取（或轉介）來源，並選取您要包含的來源。
1. 此範例使用 `stacked columns` 圖表型別。

以下是視覺化逐步解說：

![建立「依使用者來源重複訂單」報表。](../../assets/Repeat_orders_by_user_source.gif)


## 正在結束 {#wrapup}

本主題僅涉及幾個可用來分析贏取和行銷管道價值的分析，但這只是冰山一角。

## 相關 {#related}

* [透過以下方式追蹤訂單反向連結來源： [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [正在連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [建置 [!DNL Google ECommerce] 包含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [中的UTM標籤最佳實務 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
