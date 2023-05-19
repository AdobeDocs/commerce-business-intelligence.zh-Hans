---
title: 提高廣告促銷活動的ROI
description: 瞭解評估行銷活動績效的幾種不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Advertising Campaigns和ROI

[!DNL Adobe Commerce Intelligence] 讓您輕鬆進行 [結合廣告成本資料和收入資料](../../data-analyst/importing-data/integrations/google-adwords.md) 從您的資料庫。 這可協助您識別哪些行銷活動具有最高的投資報酬率(ROI)。 本主題探討評估行銷活動績效的幾個不同方法。

## 必要條件

* 匯入您的廣告成本資料：
   * [連線您的 [!DNL Google AdWords] 至 [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md)：這會同步您的 [!DNL Adwords] 支出 [!DNL Commerce Intelligence]
   * [上傳其他廣告成本資料](../importing-data/connecting-data/import-offline-ad-data.md)：建議將此用於沒有直接聯結器的頻道 [!DNL Commerce Intelligence]
   * 如果您從多個來源匯入成本資料，您可以 [consolidate](../../best-practices/consolidating-your-tables.md) 中的資料 [!DNL Commerce Intelligence]. 簡單 [提交支援票證](../../guide-overview.md#Submitting-a-Support-Ticket).
* [追蹤使用者贏取管道資料](../analysis/google-track-user-acq.md)

## 使用者贏取行銷活動

以贏取使用者為目標的行銷活動可從多個角度進行測量，包括：

1. 從行銷活動取得的新使用者人數
1. 從註冊到購買行銷活動的轉換率
1. 根據平均使用者期限值(LTV)的促銷活動ROI

上述分析(1)和(2)會在單獨的教學課程中探討，主題為 [識別您的主要行銷管道](../analysis/most-value-source-channel.md). 在這裡，您可以探索分析(3)來測量一段時間內的行銷活動ROI。 此引數可回答使用者從特定行銷活動取得的收入，是否足以支付取得成本。

>[!NOTE]
>
>此範例假設所有行銷活動成本都專門用於取得新使用者。 實際上，您的行銷活動成本也會與獲得未轉換的造訪、重複購買者等共用。 假設所有成本都用於取得新的註冊使用者，則產生的ROI會考慮最壞的情況（每次取得成本最高）。 您可以確定您的實際ROI高於您的計算。
>
>範例：假設您在產生10個新使用者和10個重複購買者的行銷活動上花費$20，則您每個新使用者的實際成本為$1。 但是，假設所有成本都花在收購新使用者上，則每次收購的成本為2美元。

**1. 首先，請建立可依促銷活動劃分廣告成本的圖表：**

1. 建立 [!UICONTROL Metric] 總和就是您在一段時間內的花費
1. 前往 [!UICONTROL Data > Metrics]
1. 選取 `Add New Metric` 並選取 [!DNL `Adwords...`] 正在錄製您的 [!DNL AdWords] 成本資料。
1. 在量度編輯器中，為您的量度命名(例如， [!UICONTROL AdWord Cost])
1. 使用下拉式清單，執行 **總和** 於 `adCost` 中的欄 [!DNL Adwords...] 表格（變更），排序依據： `date` 欄。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 按一下 `Back to Metric List` 前往頂端的任何儀表板。

1. 建立行銷活動所花費的區段報表
1. 在任何控制面板中，按一下 [!UICONTROL Add Report > Create report]
1. 選取 [!UICONTROL Adword Cost] 您剛才建立的量度
1. 設定 [!UICONTROL Time period] 至 `All-time`、和 [!UICONTROL Interval] 至 `None`
1. 在 `Group by` 標籤，新增 `campaign` 作為 [!UICONTROL grouping field]，然後按一下 `Add All` 在方塊中。
1. 此報表顯示您的所有時間 [!DNL AdWords] 成本（依行銷活動）

**2. 建立可依行銷活動計算新使用者的報表：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create report]**
1. 選取 `New users` 計算一段時間內新註冊使用者人數的量度
1. 設定 [!UICONTROL Time period] 至 `All-time`、和 [!UICONTROL Interval] 至 `None`
1. 在 `Group by` 標籤，新增 `campaign` 作為 `grouping field`，然後按一下 **`Add All`** 在方塊中
1. 此報表依行銷活動顯示您所有時間的註冊使用者

**3. 建立報表，依行銷活動對平均使用者LTV進行分段：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create report]**
1. 選取 `Average lifetime revenue` 計算平均使用者期限收入的量度
1. 設定 [!UICONTROL Time period] 至 `All-time`、和 [!UICONTROL Interval] 至 `None`
1. 在 `Group by` 標籤，新增 `campaign` 或 `utm\_campaign` 作為 [!UICONTROL grouping field]，然後按一下 `Add All` 在方塊中
1. 此報表顯示依行銷活動的平均使用者期限收入

**最後，將這三項分析整合在一份報表中，以計算行銷活動ROI：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 新增作為輸入，使用上述三個量度。 每個檔案都會指派一個字母(例如，\[`A`\]， \[`B`\]和\[`C`\])
1. [!UICONTROL Cost]：新增量度AdWords成本 — 此為變數\[A\]。 依行銷活動傳回成本。
1. [!UICONTROL Users]：新增量度新使用者 — 這是變數\[B\]。 這會傳回行銷活動的使用者人數。
1. [!UICONTROL LTV]：新增量度平均期限收入 — 此為變數\[`C`\]。 這會依行銷活動傳回LTV。

1. 按一下「圖表」一字旁邊的隱藏圖示，即可將焦點放在表格上
1. 現在使用 `Add Formula` 若要結合這些量度，如下所示：
1. [!UICONTROL ROI]：輸入公式 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，若為\[`A`\]表示 `Ad Cost by Campaigns`， \[`B`\]表示 `New users by campaigns`，和\[`C`\] `LTV by campaigns`. 這會傳回（平均使用者LTV — 每次收購的平均成本） / （每次收購的平均成本）的比率
1. [!UICONTROL Avg Return per User]：輸入公式 **\[`C`\]-(\[`A`\]/\[`B`\])**. 透過計算（平均使用者LTV） — （每次收購的平均成本），這會傳回使用者的平均利潤。
1. [!UICONTROL CPA]：輸入公式 **`\[A\]/\[B\]`**. 這會傳回實際促銷活動的每次贏取成本。
1. 要納入的其他潛在量度 [!DNL AdWords] 資料包含的總和  `Impressions` 和 `adClicks` (從 [!DNL AdWords] 資料)，以及總計 `number of orders` 透過特定行銷活動建立。
1. 根據使用者註冊或首次購買後30天和90天的LTV來計算ROI，也可能會很有趣。

1. 您可以隨時按一下並拖曳量度和公式，以重新排序報表的欄
1. 為報表命名，並請務必儲存為表格。

## 產品行銷活動

您執行產品專屬廣告嗎？ 若是如此，您可以計算特定產品的收入/成本，以評估這些促銷活動的ROI。

>[!NOTE]
>
>此範例假設所有行銷活動成本都專門用於產生特定產品的購買。 假設所有成本都花在產生購買上，則產生的ROI會考慮最壞的情況（最高每次購買成本）。 您可以確定您的實際ROI高於此計算。 範例：假設您在產生10個新使用者和10次購買的行銷活動上花費$20，您的每次購買實際成本為$1。 假設所有成本都是為了取得新使用者，則每次購買的成本為$2。

開始之前， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 若要將下列維度聯結至行專案表格(`sales\_flat\_order\_item, order\_item`)：

* 訂單的來源（如果您只追蹤使用者層級的轉介來源，則加入使用者的來源）
* 訂單的行銷活動（如果您只追蹤使用者層級的轉介來源，則加入使用者的行銷活動）
* 訂單媒體（如果您只追蹤使用者層級的轉介來源，則加入使用者的媒體）

**1. 現在先建立圖表，傳回特定產品的每個行銷活動的收入：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 選取 `Revenue by items` 計算明細行專案層級收入的量度
1. 設定 [!UICONTROL Time period] 至 `All-time`、和 [!UICONTROL Interval] 至 `None`
1. 在 `Filter by` 標籤，新增 `product name 'IN'` 產品 `A`，產品 `B`，產品 `C`， ...」，並包含以逗號分隔之促銷活動鎖定的所有產品名稱(例如， `product name 'IN' yellow t-shirt`， `red t-shirt, blue t-shirt`)
1. 在 `Group by` 標籤，新增 `order's campaign` 或 `order's utm\_campaign` 作為 `grouping` 欄位，然後按一下 **[!UICONTROL Add All]** 在方塊中
1. 此報表依行銷活動顯示特定產品的收入

**2. 若要計算ROI，請再次將量度合併到一個報表中：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 新增 `Revenue by items` 量度，依照上述特定產品報表之行銷活動中的篩選器和說明分組，然後按一下 **[!UICONTROL Hide]** 在量度的純量值下方
1. 現在新增 [!DNL AdWords Cost] 量度，依照篩選條件進行，並按來自 `Ad cost by campaigns` 報告您探索的內容： `User acquisition campaigns` 區段，然後按一下 **[!UICONTROL Hide]** 在量度的純量值下方
1. 備妥這些量度後，即可新增公式：
1. [!UICONTROL ROI]：輸入公式 `\[A\]/\[B\]`，若為 `\[A\]` 表示 `Revenue per campaign for specific product(s)` 和 `\[B\]` 表示 `Ad cost by campaigns`. 這會傳回（特定產品的收入） / （促銷活動成本）的比率
1. [!UICONTROL Return]：輸入公式 `\[A\]-\[B\]`. 這會透過計算（平均使用者LTV） — （每次收購的平均成本）傳回使用者的平均利潤
1. （可選） [!UICONTROL Revenue]：取消隱藏 `Revenue by items` 量度以瞭解每個行銷活動的特定產品收入
1. （可選） [!UICONTROL Cost]：取消隱藏 `AdWords Cost` 檢視行銷活動成本的量度

1. 為報表命名，並請務必將其儲存為表格

**3. 對每個廣告產品或產品群組重複上述步驟1和2。**

## 相關檔案

* [透過以下方式追蹤訂單反向連結來源： [!DNL Google Analytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../analysis/google-track-user-acq.md)
* [追蹤資料庫中的使用者裝置、瀏覽器和作業系統資料](../analysis/track-usr-dev-browser.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [如何 [!DNL Google Analytics] UTM歸因是否有效？](../analysis/utm-attributes.md)
* [在中進行UTM標籤的五個最佳做法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
