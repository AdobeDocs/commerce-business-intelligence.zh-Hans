---
title: 篩選器
description: 瞭解如何使用篩選器。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# 篩選器

可新增一或多個篩選器以限制用於產生報表的資料。 每個篩選器都是一個運算式，其中包含關聯表格中的欄、運運算元和值。 例如，若只要包含回頭客戶，您可以建立僅包含已下多張訂單的客戶的篩選器。 多個篩選器可以與邏輯篩選器一起使用 `AND/OR` 運運算元以新增邏輯至報表。

>[!TIP]
>
>報表最多可包含3,500個資料點。 若要減少資料點的數量，請使用篩選器來減少用於產生報表的資料量。

[!DNL Adobe Commerce Intelligence] 包含一系列篩選器，您可使用「立即可用(OOTB)」，或加以修改以符合您的需求。 您可以建立的篩選器數量沒有限制。

## 若要新增篩選器：

1. 在圖表中，暫留在每個資料點上。

   在此報表中，每個資料點會顯示當月的客戶總數。

1. 在左側面板中，按一下篩選器(![](../../assets/magento-bi-btn-filter.png))圖示。

   ![新增篩選器](../../assets/magento-bi-report-builder-filter-add.png)

1. 按一下 **[!UICONTROL Add Filter]**.

   篩選器會依字母順序編號，第一個是 `[A]`. 篩選的前兩個部分是下拉式清單選項，第三個部分是值。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 按一下篩選器的第一部分，然後選擇您要用作運算式主旨的欄。

      ![選擇篩選器的第一部分](../../assets/magento-bi-report-builder-filter-part1.png)

   * 按一下篩選器的第二個部分，然後選擇運運算元。

      ![選擇運運算元](../../assets/magento-bi-report-builder-filter-part2.png)

   * 在篩選的第三部分，輸入完成運算式所需的值。

      ![輸入值](../../assets/magento-bi-report-builder-filter-part3.png)

   * 篩選完成後，按一下 **[!UICONTROL Apply]**.

      報表現在僅包含回頭客戶，針對報表擷取的客戶記錄數已從33,000筆減少至12,600筆。

      ![已篩選的報告](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 在側邊欄中，按一下透視( ![](../../assets/magento-bi-btn-perspective.png))圖示。

   ![透視](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 在設定清單中，選擇 `Cumulative`. 然後，按一下 **[!UICONTROL Apply]**.

   ![累積透視](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   此 `Cumulative` 透檢視會隨時間分佈變化，而不是顯示每個月的鋸齒狀上下變化。

1. 輸入 `Title` ，然後按一下 **[!UICONTROL Save]** 它作為 `Chart` 至您的儀表板。

   ![儲存至控制面板](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
