---
title: 檢查更新週期狀態
description: 瞭解如何檢查更新週期狀態。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 更新週期進度

當您登入 [!DNL Adobe Commerce Intelligence] 圖示板，有數種方式可檢查您上次更新週期的狀態。 這完全取決於型別 [使用者許可權](../administrator/user-management/user-management.md) 您擁有的。

## 為何要檢查更新週期狀態？

當您稽核中的資料時，檢查狀態更新週期會很有用 [!DNL Commerce Intelligence] 帳戶。 如果您看到 [不符合您期望的結果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)例如，以下專案的每日銷售額： [!DNL Commerce Intelligence] 與您在eCommerce平台或 [[!DNL Google] 電子商務收入](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 您可以檢查最後一個資料點，以檢視問題在更新完成後是否解決。

## [!UICONTROL Read-Only] 和 [!UICONTROL Standard] 使用者

`Read-only` 使用者可以登入他們的儀表板，並透過將游標移至頁面右上角的圖示上來檢視資料最近更新的時間。 這會顯示上次提取資料點的時間。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 使用者

`Admin` 使用者可以登入控制面板，檢視上方的最後一個資料點，以及其帳戶整合的簡短狀態圖示。

如需詳細資訊，管理員使用者可以按一下 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

此頁面顯示目前的更新狀態以及上次完成更新的時間。

如果更新進行中，您會看到更新完成後要求電子郵件通知的連結。

如果更新未進行中，您會看到強制開始更新的連結。

>[!NOTE]
>
>如果您有中斷時間（您不想要的時間） [!DNL Commerce Intelligence] 更新您的資料)，強制更新會啟動不遵守這些中斷時數限制的更新週期。
