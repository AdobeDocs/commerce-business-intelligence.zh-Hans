---
title: 儀表板
description: 瞭解如何建立和使用儀表板。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 儀表板

[!DNL Adobe Commerce Intelligence] 控制面板可讓您快速檢視商店的績效和銷售活動。 個別控制面板可以與其他使用者共用，並組織成邏輯群組。 您也可以為其他使用者設定不同等級的許可權。

可以輕鬆建立報表、新增至控制面板，以及將資料匯出至Excel。 圖表和報告可以調整大小並拖曳到儀表板上的適當位置。

![儀表板](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 建立儀表板 {#createdash}

控制面板是可共用的，其主題貯體適用於您在Report Builder中建立的分析。 這就是鼓勵您的團隊共同作業，並在整個組織中維護單一信任來源的方法。

*如果您是管理員或標準使用者*，您可以按一下 `Dashboard Options` 下拉式清單並選取 `Create New dashboard`.

您所建立的控制面板完全由您決定。 您可以依照自己的需求和工作流程，以任何方式在控制面板中排列元素和調整元素大小。

![排列調整儀表板元素大小](../../assets/arrange_resize_dashboard_element.gif)

### 建立控制面板

1. 在功能表中，按一下 **[!UICONTROL Dashboards]**.

1. 預設圖示板的名稱會出現在圖示板標題的左上角。 按一下向下箭頭(![](../../assets/magento-bi-btn-down.png))以顯示可用的選項。

   ![建立儀表板](../../assets/magento-bi-dashboard-create.png)

1. 按一下 **[!UICONTROL Create Dashboard]**. 然後，執行下列動作：

   * 輸入 `Name` （適用於您的儀表板）。

   * 若要建立 `Group` 對於圖示板，輸入群組的名稱。

      例如，如果您的Commerce安裝有多個商店檢視，您可能會為每個商店檢視建立一個群組。

   * 按一下 **[!UICONTROL Create]**.

   ![儀表板名稱](../../assets/magento-bi-dashboard-create-name.png)

   * 新圖示板的名稱會出現在左上角。 按一下向下箭頭(![](../../assets/magento-bi-btn-down.png))以顯示選項。 如果您已建立群組，則新圖示板會顯示在清單中該群組的下方。


### 新增報告

1. 若要新增報表，請執行下列任一項作業：

   * 按一下 **[!UICONTROL Add a report]** 提示頁面。

   * 在控制面板標題中，按一下 **[!UICONTROL Add Report]**.

      ![新增報告](../../assets/magento-bi-dashboard-create-add-report.png)

1. 按一下 **[!UICONTROL Create Report]** 以顯示 **[!UICONTROL Report Builder Options]**.

   ![Report Builder選項](../../assets/magento-bi-report-builder.png)

## 在儀表板上排列專案

* 若要調整圖表或報表的大小，請將右下角拖曳至新大小。

* 若要移動圖表或報表，請將滑鼠指標暫留在標題或標題上，直到游標變成十字形。 然後，將其拖曳到適當位置。

## 管理您的儀表板 {#managedash}

在 **[!DNL Manage Data** > **Dashboards]**，您可以管理自己所擁有控制面板的使用者許可權、刪除不再需要的控制面板，以及設定預設控制面板。

### 共用您的儀表板 {#sharingdash}

達到真正規模 [!DNL Commerce Intelligence] 在整個組織並提供有價值的深入分析，Adobe鼓勵您與其他團隊成員共用您建立的儀表板。 *您可以共用您擁有的儀表板* 按一下 `Share Dashboard` 選項。

當您共用控制面板時，您可以在組織或個人基礎上指派許可權，這表示您可以決定誰可以檢視和編輯您的報告。

>[!NOTE]
>
>`Read-Only` 使用者只有直接共用給他們的儀表板存取權 — 他們無法自行搜尋和新增儀表板。 別忘了把它們放在回圈中！

### 存取共用儀表板 {#accessshared}

*如果您是管理員或標準使用者* 且想要將共用儀表板新增至您的帳戶，您可以按一下 **[!UICONTROL Dashboard Options]** 然後按一下 **[!UICONTROL Find]** 在下拉式清單中。

![尋找儀表板](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 管理儀表板設定

1. 在功能表中，按一下 **[!DNL Manage Data** > **Dashboards]**.

1. 如果適用，請輸入新的 `Dashboard Name`.

1. 若要將控制面板指派給特定 `Dashboard Group`，從群組清單中選擇。

   **`Permissions`**

   若要為所有使用者授予控制面板的相同存取層級，請執行下列動作：

   1. 下 **`Shared with`**，選擇下列其中一個選項：

      * `View`
      * `Edit`
      * `None`
   1. 提示確認時，按一下 **[!UICONTROL OK]** 更新每個使用者的許可權層級。

   1. 若要變更個人的許可權層級，請在清單中尋找使用者以變更許可權層級。 變更會自動儲存。

   **`Default`**

   1. 若要將此儀表板設為您的預設儀表板 [!DNL Commerce Intelligence] 帳戶，按一下 **[!UICONTROL Make Default]**.

   **`Remove`**

   1. 若要移除儀表板，請按一下 **[!UICONTROL Delete Dashboard]**.
