---
title: 連線Google Analytics倉儲
description: 瞭解如何追蹤訪客如何使用您的網站、哪些內容吸引人、訪客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 连接 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [ 管理员权限 ](../../../administrator/user-management/user-management.md) 。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是 internet 上使用最广泛的网站分析服务。 通过在您的网站实施 [!DNL Google Analytics] ，您可以跟踪访客使用网站的方式、哪些内容有吸引力、访客退出的位置等。 [!DNL Google Analytics Warehoused] 是与现有 [!DNL Google Analytics] 集成的独立集成。 由于您的数据仓库中的 [!DNL Google Analytics] 数据与现有 [!DNL Google Analytics] 集成的实时馈送不同，因此它可以更好地分析。 在中 [!DNL Commerce Intelligence] 分析这些量度以及其他数据，可改进网站的整体运行状况和可用性。

## GA Warehoused 与实时集成之间的差异

主要區別在於儲存了一項整合([!DNL Google Analytics Warehoused])，而另一個不是([!DNL Google Analytics Live])。 若為 [!DNL Google Analytics Warehoused]，這允許操控您的 [!DNL Google Analytics] 資料並提供您合併 [!DNL Google Analytics] 和其他資料來源，以建立具洞察力的報表。

檢視 [!DNL Google Analytics] 廣告行銷活動，以從操作角度說明可執行的動作。 假設您在第四季有多個名稱不同的廣告行銷活動。 行銷活動是特定行銷計畫的成果。 使用倉儲資料，您可以建立欄以尋找有問題的行銷活動名稱，並傳回的第四季行動方案名稱 `Operation Dumbo`.

組合外觀允許 [!DNL Google Analytics] 要與其他資料結合以進行分析的資料。 例如， `Total Time On Site By Ad Campaign` 从 [!DNL Google Analytics] 获取数据并将其与 `Total Spent Per Campaign` 数据 [!DNL Facebook Ads] 进行联接，以完整了解参与的成本。

[!DNL Google Analytics Live]通过整合，每个 [!DNL Google Analytics] 图表都点赞一个小的思洛存储器，而该存储库未保存在您的数据仓库中。

## 连接 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是一个 `Premium` 集成。 [如果您有兴趣将此集成添加到您的订阅，请联系支持人员 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 。

1. 转到下 **[!UICONTROL Admin** > **Integrations]** 的 `Connections` 页面。
1. 按一下 **[!UICONTROL Add an Integration]**，位於右側。
1. 按一下 [!DNL Google Analytics Warehoused] 圖示。 如此將可開啟 [!DNL Google Analytics] 認證頁面。
1. 輸入您的 [!DNL Google Analytics] 認證。 授權程式完成後，您會被重新導向回 [!DNL Commerce Intelligence].
1. 設定檔ID清單隨即顯示。 檢查您要連線的設定檔 [!DNL Commerce Intelligence]. 如果您有多個設定檔，並且需要一些幫助來識別哪一個，請參閱連線多個 [!DNL Google Analytics] 下方的設定檔區段。

## 连接多个 [!DNL Google Analytics] 配置文件

您可以将多个网站连接到单个 [!DNL Google Analytics] 帐户，并由其自身 [!DNL Google Analytics] 的用户档案 ID 进行标识。 在这种情况下，您可以选择将您的所有用户档案 Id 都包含在中 [!DNL Commerce Intelligence] 。 检查在 &quot;用户档案选择&quot; 步骤中要点赞包含的用户档案 Id。

识别特定网站的 [!DNL Google Analytics] 配置文件 ID：

1. 登录 [!DNL Google Analytics]
1. 前往特定網站的 [!DNL Google Analytics] 儀表板
1. 檢視URL — 設定檔ID對應至下列八個數字 `p` 行尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 中斷連線 [!DNL Google Analytics Warehoused] 從 [!DNL Commerce Intelligence] {#disconnect}

1. 造訪您的 [!DNL Google Analytics] [帳戶設定](https://myaccount.google.com/intro) 頁面。
1. 在 `Security` 區段，然後按一下 **[!UICONTROL edit]** 旁邊 `Authorizing` 應用程式和網站。
1. 按一下 **[!UICONTROL revoke access]** 旁邊 [!DNL Commerce Intelligence].

## 相关文档

* [Reauthenticating 集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用  [!DNL Google Analytics]  cookie 跟踪用户客户获取数据](../../analysis/google-track-user-acq.md)
