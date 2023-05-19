---
title: 限制量度存取
description: 瞭解如何使用量度存取和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 管理量度使用者

除了設定使用者許可權層級外，您也可以逐個使用者限制量度的存取權。 例如，如果您希望會計部門能存取收入相關量度，但不存取使用者贏取量度，則可以限制這些量度的存取權。

在這樣的情況下，Adobe建議將該使用者的帳戶設定為 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 應授予不需要建立或變更量度、計算欄、整合或使用者的許可權，但他們確實需要存取Data Warehouse中的資料。 如果您想要完全限制對資料的存取，請使用 **[!UICONTROL Read Only]** 許可權。

設定許可權層級後，您可以選取 **[!UICONTROL Standard]** 使用者可以執行下列動作來存取：

1. 前往 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 選取所需的使用者帳戶。
1. 此 **[!UICONTROL Metrics]** 索引標籤會顯示可用量度的清單。 檢查您希望使用者存取的量度，並取消選取使用者不應該存取的量度。
1. [!DNL Adobe Commerce Intelligence] 會自動儲存變更。 如果變更成功， [!DNL Commerce Intelligence] 顯示 **[!UICONTROL Saved!]** ，位於頁面頂端。

>[!NOTE]
>
>所有使用者具有 **[!UICONTROL Standard]** 除了來自的所有量度之外，許可權還可以透過「資料匯出」存取Data Warehouse中的所有資料 [!DNL Google Analytics].

您也可以編輯量度和 **[!UICONTROL Standard]** 在中選取使用者 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 區段。

>[!NOTE]
>
>如果您複製量度， [!DNL Commerce Intelligence] 複製在原始量度中設定的使用者許可權。
