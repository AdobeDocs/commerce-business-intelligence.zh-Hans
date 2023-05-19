---
title: 連線Google Analytics倉儲
description: 瞭解如何追蹤訪客如何使用您的網站、哪些內容吸引人、訪客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是網際網路上使用最廣泛的網站分析服務。 實作 [!DNL Google Analytics] 「在您的網站上」可讓您追蹤訪客如何使用您的網站、哪些內容吸引人、訪客在哪裡退出等等。 [!DNL Google Analytics Warehoused] 是與您現有的獨立整合 [!DNL Google Analytics] 整合。 由於具備以下功能，因此可更好地進行分析 [!DNL Google Analytics] Data Warehouse中的資料，這與現有的即時摘要不同 [!DNL Google Analytics] 整合。 在中分析這些量度 [!DNL Commerce Intelligence]，連同其他資料片段，可改善您網站的整體健全度和可用性。

## GA倉儲與即時整合的差異

主要區別在於儲存了一項整合([!DNL Google Analytics Warehoused])，而另一個不是([!DNL Google Analytics Live])。 若為 [!DNL Google Analytics Warehoused]，這允許操控您的 [!DNL Google Analytics] 資料並提供您合併 [!DNL Google Analytics] 和其他資料來源，以建立具洞察力的報表。

檢視 [!DNL Google Analytics] 廣告行銷活動，以從操作角度說明可執行的動作。 假設您在第四季有多個名稱不同的廣告行銷活動。 行銷活動是特定行銷計畫的成果。 使用倉儲資料，您可以建立欄以尋找有問題的行銷活動名稱，並傳回的第四季行動方案名稱 `Operation Dumbo`.

組合外觀允許 [!DNL Google Analytics] 要與其他資料結合以進行分析的資料。 例如，take `Total Time On Site By Ad Campaign` 資料來源 [!DNL Google Analytics] 並加入其中 `Total Spent Per Campaign` 資料來源 [!DNL Facebook Ads] 以全面瞭解您所需的業務開發成本。

使用 [!DNL Google Analytics Live] 另一方面，整合的每一 [!DNL Google Analytics] 圖表就像是不會儲存在Data Warehouse中的小型筒倉。

## 正在連線 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是 `Premium` 整合。 [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果您有興趣將此整合新增至您的訂閱。

1. 前往 `Connections` 頁面於 **[!UICONTROL Admin** > **Integrations]**.
1. 按一下 **[!UICONTROL Add an Integration]**，位於右側。
1. 按一下 [!DNL Google Analytics Warehoused] 圖示。 如此將可開啟 [!DNL Google Analytics] 認證頁面。
1. 輸入您的 [!DNL Google Analytics] 認證。 授權程式完成後，您會被重新導向回 [!DNL Commerce Intelligence].
1. 設定檔ID清單隨即顯示。 檢查您要連線的設定檔 [!DNL Commerce Intelligence]. 如果您有多個設定檔，並且需要一些幫助來識別哪一個，請參閱連線多個 [!DNL Google Analytics] 下方的設定檔區段。

## 連線多個 [!DNL Google Analytics] 設定檔

您可能有多個網站連線至單一 [!DNL Google Analytics] 帳戶，由其自身識別 [!DNL Google Analytics] 設定檔ID。 在此情況下，您可以選擇將您的所有設定檔ID納入 [!DNL Commerce Intelligence]. 檢查您要在設定檔選取步驟中包含的設定檔ID。

識別特定網站的 [!DNL Google Analytics] 設定檔ID：

1. 登入 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 檢視URL — 設定檔ID對應至下列八個數字 `p` 行尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 中斷連線 [!DNL Google Analytics Warehoused] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://myaccount.google.com/intro) 頁面。
1. 在 `Security` 區段，然後按一下 **[!UICONTROL edit]** 旁邊 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 旁邊 [!DNL Commerce Intelligence].

## 相關檔案

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在連線 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析網站活動和客戶轉換率](../../analysis/web-act-cust-conversion.md)
* [使用追蹤使用者贏取資料 [!DNL Google Analytics] Cookie](../../analysis/google-track-user-acq.md)
