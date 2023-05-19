---
title: 管理您的帳戶設定
description: 瞭解如何為您的Data Warehouse自訂帳戶設定。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 自訂帳戶設定

>[!NOTE]
>
>需要 [管理員許可權。](../../administrator/user-management/user-management.md)

在您的 [!DNL Commerce Intelligence] 帳戶，您可以為Data Warehouse自訂帳戶設定。 您可以在任何畫面的右上角選取您的組織名稱，然後選擇 **[!UICONTROL Account Settings]** 下拉式清單中的。

* **[!UICONTROL Client Name:]** 此設定會出現在所有儀表板的右上角，以及您帳戶內的其他位置。 如果您想要變更 **[!UICONTROL "Vandelay Industries Co., Ltd]** 轉換成 **[!UICONTROL "Vandelay]**，這是執行此動作的位置。

* **[!UICONTROL Currency:]** 這是 *預設貨幣* 您帳戶中的所有貨幣值。 無論小數或貨幣值何時同步至Data Warehouse，此設定都會決定報表中置於該值之前的符號。

* **[!UICONTROL Blackout Hours:]** 此設定可確保您的Data Warehouse在一天中的選定時段不會存取您連線的資料庫。 所有時數都會以零時和東部標準時間(EST)表示。 例如，如果您不想在東部標準時間上午9:00到下午1:00之間存取生產資料庫，則應輸入下列數字陣列： **9、10、11、12**.

* **[!UICONTROL Forced update hours:]** 此設定可確保帳戶中的Data Warehouse更新自動開始 *在小時內* 您已指定。 和中斷時數一樣，這些也會出現在ET中。 例如，如果您希望Data Warehouse更新自動從 **午夜** 和 **中午** EST，您應輸入下列位數陣列： **0， 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此選項可管理排程傳送電子郵件摘要的情況 *在其其中一個報表中的資料之前* 已重新整理。 如果您選擇 **否**，您的帳戶會在排程的時間略過傳送電子郵件。 而是在您的資料更新後，由您的帳戶傳送。 如果您選擇 **[!UICONTROL Yes]**，您的帳戶會傳送電子郵件、包含說明資料已過時的訊息，並在資料更新後傳送另一封電子郵件。

* **[!UICONTROL Enable data updates:]** 此選項可確保資料更新在您的帳戶上執行。 如果您將設定變更為 **[!UICONTROL No]**，資料同步和欄計算會在您的帳戶中暫停。

>[!NOTE]
>
>請務必選取 **[!UICONTROL Save Customizations]** 完成任何變更之後。
