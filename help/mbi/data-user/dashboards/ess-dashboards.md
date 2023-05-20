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

[!DNL Adobe Commerce Intelligence] 控制面板可讓您快速檢視商店的績效和銷售活動。 個別控制面板可以與其他使用者共用，並組織成邏輯群組。 您还可以为其他用户设置不同级别的许可。

可以輕鬆建立報表、新增至控制面板，以及將資料匯出至Excel。 圖表和報告可以調整大小並拖曳到儀表板上的適當位置。

![儀表板](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 建立儀表板 {#createdash}

控制面板是可共用的，其主題貯體適用於您在Report Builder中建立的分析。 這就是鼓勵您的團隊共同作業，並在整個組織中維護單一信任來源的方法。

*如果您是管理员或标准用户* ，则可以通过单击下拉列表并选择 `Create New dashboard` &quot;&quot; `Dashboard Options` 来创建功能板。

您所建立的控制面板完全由您決定。 您可以依照自己的需求和工作流程，以任何方式在控制面板中排列元素和調整元素大小。

![排列調整儀表板元素大小](../../assets/arrange_resize_dashboard_element.gif)

### 建立控制面板

1. 在功能表中，按一下 **[!UICONTROL Dashboards]**.

1. 默认功能板的名称显示在功能板标题的左上角。 单击向下箭头（ ![](../../assets/magento-bi-btn-down.png) ）以显示可用的选项。

   ![创建功能板](../../assets/magento-bi-dashboard-create.png)

1. 单击 **[!UICONTROL Create Dashboard]** 。 然后，执行以下操作：

   * `Name`为您的功能板输入。

   * 要为功能板创建 `Group` ，请输入群组的名称。

      例如，如果您的Commerce安裝有多個商店檢視，您可能會為每個商店檢視建立一個群組。

   * 按一下 **[!UICONTROL Create]**.

   ![儀表板名稱](../../assets/magento-bi-dashboard-create-name.png)

   * 新功能板的名称将显示在左上角。 按一下向下箭頭(![](../../assets/magento-bi-btn-down.png))以顯示選項。 如果创建了群组，则新功能板会显示在列表中的群组下方。


### 新增報告

1. 若要新增報表，請執行下列任一項作業：

   * 按一下 **[!UICONTROL Add a report]** 提示頁面。

   * 在控制面板標題中，按一下 **[!UICONTROL Add Report]**.

      ![新增報告](../../assets/magento-bi-dashboard-create-add-report.png)

1. 按一下 **[!UICONTROL Create Report]** 以顯示 **[!UICONTROL Report Builder Options]**.

   ![Report Builder 选项](../../assets/magento-bi-report-builder.png)

## 在儀表板上排列專案

* 若要調整圖表或報表的大小，請將右下角拖曳至新大小。

* 若要移動圖表或報表，請將滑鼠指標暫留在標題或標題上，直到游標變成十字形。 然後，將其拖曳到適當位置。

## 管理您的儀表板 {#managedash}

在中 **[!DNL Manage Data** > **Dashboards]** ，您可以为您拥有的功能板管理用户权限，删除不再需要的功能板，并设置默认功能板。

### 共享您的功能板 {#sharingdash}

为了真正地在整个组织范围内扩展 [!DNL Commerce Intelligence] 并提供有价值的见解，Adobe Systems 鼓励您共享用其他团队成员创建的功能板。 *您可以通过单击 `Share Dashboard` 页面顶部的选项来共享自己* 的功能板。

共享功能板时，您可以在整个组织或单个基础上分配权限，这意味着您可决定谁可以视图和编辑报表。

>[!NOTE]
>
>`Read-Only` 用户只能访问直接与他们共享的功能板-他们不能搜索，也不能添加控制面板。 別忘了把它們放在回圈中！

### 存取共用儀表板 {#accessshared}

*如果您是管理員或標準使用者* 且想要將共用儀表板新增至您的帳戶，您可以按一下 **[!UICONTROL Dashboard Options]** 然後按一下 **[!UICONTROL Find]** 在下拉式清單中。

![尋找儀表板](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 管理功能板设置

1. 在菜单上，单击 **[!DNL Manage Data** > **Dashboards]** 。

1. 如果适用，请输入新 `Dashboard Name` 的。

1. 若要將控制面板指派給特定 `Dashboard Group`，從群組清單中選擇。

   **`Permissions`**

   若要為所有使用者授予控制面板的相同存取層級，請執行下列動作：

   1. 下 **`Shared with`**，選擇下列其中一個選項：

      * `View`
      * `Edit`
      * `None`
   1. 提示確認時，按一下 **[!UICONTROL OK]** 更新每個使用者的許可權層級。

   1. 要更改个人的许可级别，请在列表中找到用户更改许可级别。 更改会自动保存。

   **`Default`**

   1. 要将此功能板设为 [!DNL Commerce Intelligence] 帐户的默认功能，请单击 **[!UICONTROL Make Default]** 。

   **`Remove`**

   1. 要删除功能板，请单击 **[!UICONTROL Delete Dashboard]** 。
