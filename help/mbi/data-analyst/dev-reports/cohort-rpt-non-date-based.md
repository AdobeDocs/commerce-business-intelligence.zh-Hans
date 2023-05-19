---
title: 非日期同類群組的同類群組Report Builder
description: 瞭解如何依類似活動或屬性將使用者分組。
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] 以非日期為基礎的同類群組

此 [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 很適合協助商戶研究不同使用者子集在一段時間內的行為。 在過去， `Cohort Report Builder` 已最佳化為依一般使用者分組 `cohort date` （例如，在指定月份首次購買的所有客戶集）。 此 `Non-Date Based Cohort` 功能現在可讓您依據類似活動或屬性來群組使用者。 檢視此功能的幾個使用案例。

## 使用案例

這不是一份完整的清單，但以下是一些使用此功能可完成的潛在分析。

* 檢查從以下專案取得的客戶收入： [!DNL Google] 與 [!DNL Facebook]
* 分析首次購買地點為美國與加拿大的客戶
* 檢視從各種廣告促銷活動取得的客戶行為

## 如何建立分析

1. 按一下 **[!UICONTROL Report Builder]** 在左側標籤上或 **[!UICONTROL Add Report** > **Create Report]** 在任何儀表板中。

1. 在 `Report Builder Selection` 熒幕，按一下 **[!UICONTROL Create Report]** 旁邊 `Visual Report Builder` 選項。

### 新增量度

現在您已在 `Report Builder`，您可新增要對其執行分析的量度(例如： `Revenue` 或 `Orders`)。

>[!NOTE]
>
>原生 [!DNL Google Analytics] 量度與 `Cohort Report Builder`. 此範例的目標是檢視透過不同方式取得的第一筆訂單客戶在一段時間內的收入 [!DNL Google Analytics] 來源。

### 切換 `Metric View` 至 `Cohort`

![同類群組1切換量度檢視](../../assets/1-toggle-metric-view-to-cohort.png)

這會開啟一個新視窗，您可在其中設定同類群組報表的詳細資料。

建立同類群組報表需要五種規格：

1. 如何將同類群組分組
1. 選取同類群組
1. 動作時間戳記
1. 同類群組首次動作時間範圍
1. 同類群組發生後的時間範圍

![同類群組群組](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->

!![cohort-first-action-time-range]<!--(../../assets/3-cohort-first-action-time-range.png){: width="400" height="554"}-->

#### 1.分組 `cohorts`

`Cohorts` 在此範例中，依行為特徵分組 `Customer's first order GA source`. 此處可用的選項是已經指定為的欄 `groupable` 量度的。

#### 2.選取同類群組

您可以顯示給定特徵的所有結果。 因為這會導致許多 `cohorts`，您可以選取 `cohorts` (對應至下列專案可用的各種值： `Customer's first order GA source`)。

![同類群組群組](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

這可讓您選擇以日期為基礎的欄，而不是建立量度的欄。 在下方，您會看到選取適用於指定的時間範圍 `action timestamp`.

#### 4. `Cohort first action time range`

您可以在此處選取包含 `cohorts action timestamp` （首次訂購時間為2017年11月至2018年10月的客戶亦是如此）。 這可以是移動日期範圍或固定日期範圍。

#### 5. `Time range after cohort occurrence`

您想看看 `cohorts` 按月、周或年顯示一段期間？ 您可在這裡進行這些選取。 在該區段下方，您將選取 `time range` 晚於 `cohort action timestamp` 已發生。 例如，對於在動作時間範圍內下第一筆訂單的客戶，這會向您顯示12個月的資料。

![cohort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] 當您在兩者之間切換時，套用至量度的功能會維持不變 `Standard` 和 `Cohort` 檢視。

### 相關

另請參閱 [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
