---
title: 連線Adobe Analytics
description: 瞭解如何集中端對端客戶歷程的重點 [!DNL Adobe Analytics] 以及您賴以信賴的電子商務焦點 [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

此 [!DNL Adobe Analytics] 整合 [!DNL Adobe Commerce Intelligence] 可讓您集中對端對端客戶歷程的關注 [!DNL Adobe Analytics] 以及您賴以信賴的電子商務焦點 [!DNL Commerce Intelligence]. 這可讓您全面瞭解商店的整體效能。

更具體地說， [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence] 提供商戶開始合併的功能 [!DNL Adobe Commerce] 和 [!DNL Adobe Analytics] 資料集。

- 從您現有的建立連線 [!DNL Adobe Analytics] 帳戶至 [!DNL Commerce Intelligence].

- 從單一報表套裝中選取最多25個量度和維度，以復寫至您的Data Warehouse。

- 使用所有標準 [!DNL Commerce Intelligence] 轉換、加入及報告復寫資料的功能 [!DNL Adobe Analytics] 資料。

## 連線先決條件

需要下列資訊才能進行連線：

- [!DNL Adobe Analytics] 登入認證

- `Name` 和/或 `ID` 之 [!DNL Adobe Analytics] 要從中複製資料的報表套裝

- 要復寫到的量度和維度清單 [!DNL Commerce Intelligence]

## 連線 [!DNL Adobe Analytics] 整合 [!DNL Commerce Intelligence]

1. 前往 `Integrations` 頁面於 **[!DNL Manage Data** > **Integrations]**.

1. 按一下 **[!UICONTROL Add an Integration]**.

1. 按一下 **[!UICONTROL Adobe Analytics]** 圖示來存取可讓您授權 [!DNL Adobe Analytics] 帳戶連線。

1. 按一下 **[!UICONTROL Authorize with Adobe Analytics]**.

1. 輸入您的 [!DNL Adobe Analytics] 認證。 成功授權後，您會被重新導向回 [!DNL Commerce Intelligence].

1. 可用的報表套裝清單隨即顯示。 選取您要匯入資料的來源報表套裝，然後按一下 **[!UICONTROL Continue]**.

1. 度量和維度選擇畫面隨即顯示。 請至少選取一個量度和至少一個維度，最多可合併總共25個量度和維度。 依名稱搜尋或捲動以尋找元件，然後按一下核取方塊以選取。 按一下 **[!UICONTROL Continue]**.

1. 選取的報表套裝會顯示在表格中。 按一下 **[!UICONTROL Save]** 以確認您的選取。

1. 通知 [!DNL Commerce Intelligence] [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 您的整合已獲得授權，且他們會為您執行初始連線程式。

初始連線程式執行後，您的表格將可在Data Warehouse頁面的 `All Tables` 標籤。 選取您要復寫的欄，資料將在下一次完整更新後顯示。
