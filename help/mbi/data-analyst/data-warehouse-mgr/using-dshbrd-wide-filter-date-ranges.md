---
title: 儀表板範圍篩選
description: 瞭解如何在特定儀表板上大量編輯所有報告。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 儀表板範圍篩選

透過控制面板範圍的篩選，您可以對特定控制面板上的所有報告進行大量編輯。 您可以快速檢視不同時段或不同商店的相同分析。 您可以輕鬆比較每個商店去年、月或周的績效。 您可以更新整個儀表板，以因應新啟動的行銷活動。

## 日期篩選器

若要變更儀表板上報告的日期範圍或間隔，請按一下右上角的日曆圖示(![行事曆](../../assets/calendar-button.png))。

您可以選擇使用檢視資料 `Fixed Date Range` 或各種預先計算的 `Moving Date Ranges`：

![移動日期範圍](../../assets/moving_date_ranges.png)

此 `Last Full...` 移動範圍選項代表最近完全完成的範圍，而 `This...` 是目前進行中的範圍。 例如，如果現在是六月， `Last Full Month` 是 _5月1日至5月31日_，而 `This Month` 是 _6月1日至現在_.

或是建立您自己的 `Custom Moving Range`\：

![自訂移動範圍](../../assets/custom-moving-range.png)

選擇以變更間隔。 選取預設按鈕(![時間間隔預設值](../../assets/time_interval_default.png))表示只有日期範圍會變更：

![時間間隔](../../assets/time_interval.png)

若要將所有報表還原成其初始日期範圍和間隔，請按一下 **[!UICONTROL Restore Defaults]** 或按 **[!UICONTROL Cancel]**.

當您為儀表板指定日期篩選器時，該篩選器只會套用到該儀表板。 當您導覽至其他儀表板時，不會套用它。

>[!NOTE]
>
>目前， `Cohort Reports` 和 `SQL Reports` 在儀表板層級套用變更時未包含。

## 存放區篩選器

若要分析特定商店的表現，請按一下右上角的商店圖示(![存放區篩選器](../../assets/store-filter.png))。 依預設， `Store Filter` 設為 `All Stores`，會顯示來自所有使用者的資料 [存放區檢視](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) 可在您的Commerce網站上取得。

>[!NOTE]
>
>商店篩選器已針對整個啟用或停用 [!DNL Commerce Intelligence] 帳戶。 如果儀表板包含不受篩選器影響的報表（例如未在任何上建置的報表） [!DNL Adobe Commerce] 資料)，這些報表在套用商店篩選時不會更新。 您可以 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果您認為報表應該根據商店選擇進行更新，或是您認為您的帳戶商店篩選條件遭到錯誤停用。

當您從以下專案選取商店時： `Store Filter`，當您在儀表板之間導覽時，篩選器會保留您的選擇。 保留您的選取範圍可讓您檢視所選商店中任何位置的資料，直到您選取為止 `All Stores`.

## 共用儀表板的篩選器

對於共用控制面板，如果一位使用者設定日期篩選器，則具有該控制面板存取許可權的其他使用者會看到套用的相同篩選器。 不過，在此情況下不會套用商店篩選。 如果控制面板擁有者設定商店篩選並共用控制面板，則設定的商店篩選不會保留給其他使用者。 使用者必須具備 [編輯存取權](../../data-user/dashboards/share-dashboard-with-users.md) 至控制面板，以調整控制面板篩選器。
