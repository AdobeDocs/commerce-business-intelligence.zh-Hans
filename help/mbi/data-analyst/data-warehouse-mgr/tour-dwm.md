---
title: Data Warehouse管理員
description: 瞭解如何管理表格和欄同步設定、深入研究表格的綱要，以及建立要在報告中使用的計算欄。
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: c4094e780f83255846520d18f4d0806b1dd9a9ef
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Data Warehouse管理員

>[!NOTE]
>
>需要 [管理員許可權](../../administrator/user-management/user-management.md)

Data Warehouse管理員，按一下 **[!UICONTROL Manage Data > Data Warehouse]**，是您網站的入口網站 [!DNL Adobe Commerce Intelligence] Data Warehouse。 使用「Data Warehouse管理員」，您可以管理表格和欄同步設定、深入研究表格的綱要，以及建立要在報表中使用的計算欄。

本主題涵蓋：

* [瞭解如何解決問題](#learning)
* [正在同步表格和欄](#syncing)
* [建立計算欄](#calculated)
* [刪除資料表及移除資料行](#delete)
* [在背景同步新表格](#syncnew)
* [那麼，我何時可以使用新欄呢？](#when)

## 瞭解如何解決問題 {#learning}

左側 `Data Warehouse Manager` 頁面包含表格清單，可讓您輕鬆在表格之間切換。 當您從清單中選取表格時，表格管理區域會填入您可以修改所選表格的表格綱要。

在表格清單中，表格會依其連線來源分組。 這些來源新增至 [!UICONTROL Manage Data > Integrations] 而且可能是資料庫、 [API](https://developer.adobe.com/commerce/services/reporting/)或協力廠商聯結器。 在表格清單頂端有一個搜尋方塊，可讓您輕鬆尋找所需的表格。

在搜尋方塊下方，您會看到兩個選項： `All Tables` 和 `Synced Tables`. 此 `All Tables` 選項會列出您對Data Warehouse可用的所有表格，包括已同步和未同步的表格。

此 `Synced Tables` 選項會顯示所有已新增至Data Warehouse的表格，以及已從選取的資料欄復寫資料的表格。

在中看不到您要尋找的表格 `All Tables` 清單？ 這種情況有幾個可能的原因：

* 資料來源尚未新增
* 資料來源為資料庫，且 [!DNL Commerce Intelligence] 您建立的使用者沒有存取權。 在這種情況下，您或您的資料庫管理員必須授予存取權。
* 資料來源或資料表最近已新增，但尚未同步

## 正在同步表格和欄 {#syncing}

### 正在同步新資料表與原生資料行

「Data Warehouse管理員」不僅可讓您輕鬆檢視和管理資料來源，也可讓您自由選取要同步的個別表格和欄。

1. 按一下 `All Tables` 選項並找到您要同步的表格。
1. 按一下表格的名稱以預覽架構。 如果表格是新的，則所有欄會顯示為 `Unsynced`.
1. 核取您要同步的欄。

   >[!NOTE]
   >
   >表格的原生資料欄包含來自資料庫的 `Location` 欄。

1. 請務必檢查 `Primary Key` 欄 — 這些欄在欄名稱旁有一個鍵符號。 A `Primary Key` 需要將資料正確同步至Data Warehouse。

   如果您正在同步直接從資料庫取得的表格，則可能 `Primary Keys` 不可表示。 在此情況下，請連絡您的資料庫管理員，要求將一個或多個主索引鍵新增至表格。
1. 完成後，按一下 ![按鈕](../../assets/button.png) 按鈕。

A *成功！* 訊息隨即顯示，且狀態變更為 `Pending` 選取的欄。 下次完整更新完成後，新同步的表格和欄即可在報告中使用。 您也可以設定新的 [復寫方法](./cfg-replication-methods.md) 初次同步之後。

以下快速瀏覽整個程式：

![新增欄至您的Data Warehouse](../../assets/DW_sync.gif)

### 在背景同步新表格 {#syncnew}

第一次同步大型表格時，您的Data Warehouse必須先回溯擷取表格中的所有資料點，才能持續擷取新資料。 如果您的表格很大，您可能不想讓初始同步處理依序執行， **更新週期**. 在此情況下，您希望初始同步在背景中進行，在 *平行* 任何目前執行中的更新。

若要確保發生，您應選取 `Save and Sync Data Immediately` 選項第一次同步該表格。

### 檢查新表格和欄 {#forceupdate}

在新增來源、表格或欄時，您的Data Warehouse不會自動偵測這些來源、表格或欄。 同步處理會在一週中執行，以尋找新的加入專案並讓它們可用，但如果您想在程式執行之前存取新加入的表格和欄，則可以強制進行結構同步。

在表格清單的搜尋列下方是 `Check for new tables and columns` 連結。 按一下此連結會強制啟動結構同步程式；新專案通常在10分鐘後提供。 重新整理頁面以檢視新的來源、表格或欄。

## 建立計算欄 {#calculated}

只要能夠檢視和管理您所有來源的資料，就能更輕鬆深入瞭解您的業務。 但在「Data Warehouse管理員」中，您可以在表格內建立計算欄來更進一步。 `Calculated` 欄會從您現有的資料衍生出新資訊。

說您想新增 `user's lifetime revenue` 至您的 `users` 以尋找高價值使用者的表格。 或者，如果您想要依性別劃分收入，可以新增 `customer's gender` 至您的 `orders` 表格。

如需詳細資訊，請檢視此 [教學課程](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## 刪除表格和移除欄 {#delete}

就像您可以選取要同步至Data Warehouse的表格和欄一樣，您也可以拖放或移除它們。

>[!NOTE]
>
>刪除表格或移除欄會在您確認刪除後，刪除任何相依的報表、量度、篩選器集和欄。 確定您要執行此動作 —  **此動作無法復原。**

如果您按一下，請不要擔心 **[!UICONTROL Delete]** 純屬意外。 相依性檢查會在任何專案刪除前執行，因此您有機會在確認前檢閱所有專案。

若要移除欄，請按一下該欄所屬的表格。 核取您要移除的欄，然後按一下 ![button\_1.png](../../assets/button_1.png) 按鈕。

若要移除同步的表格，請選取表格中的所有欄，然後再次按一下 ![按鈕](../../assets/button_1.png) 按鈕。 這會從您的Data Warehouse中移除使用此表格的所有原生欄和計算欄。

### 確認變更

無論您是要刪除表格還是移除欄，相依性檢查都會在刪除程式完成之前執行。 相依性是指使用要移除之表格或欄的計算欄、量度、篩選器集和報表。 任何發現的相依性都會顯示 — 此時，您可以取消程式或按一下 **[!UICONTROL Confirm Changes]** 以放置表格/移除欄。

雖然已刪除的相依性無法還原，但如果您日後需要重新同步任何原生欄，表格和欄仍然可用。

以下為移除欄的快速檢視：

![從Data Warehouse移除欄](../../assets/DW_delete.gif)

## 那麼，我何時可以使用新欄呢？ {#when}

新的同步欄和新的/更新的計算欄將在下一次完整更新完成後準備使用。 如果更新尚未進行，您可以按一下「 」以強制更新 **[!UICONTROL Force update]** 顯示在頂端 `Data Warehouse` 或 `Integrations` 頁面。 您也可以按一下「 」，排程更新完成時的電子郵件通知 **[!UICONTROL Email me when complete]**.

當您準備好在報告中使用新欄時， [您需要先將量度新增至量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md). 雖然在更新完成之前無法取得資料，您仍然可以在報表中使用新欄。 更新完成後，會顯示報表中的資料。

## 正在結束

本文涵蓋許多內容。 到現在為止，您應該已經清楚瞭解什麼是資料庫、資料的組織方式、表格之間的關聯方式，以及您可以使用Data Warehouse管理員做什麼。

透過以下方式測試您的知識： [建立計算欄](../data-warehouse-mgr/creating-calculated-columns.md) 或 [製作一些有趣的報告](../../tutorials/using-visual-report-builder.md).
