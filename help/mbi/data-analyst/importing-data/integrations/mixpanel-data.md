---
title: 預期Mixpanel資料
description: 探索您可以從Mixpanel匯入的主要資料表 [!DNL Commerce Intelligence] 帳戶。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 預期 [!DNL Mixpanel] 資料

晚於 [您已連線 [!DNL Mixpanel] 帳戶](../integrations/mixpanel.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤相關資料欄位以供分析。

本主題會探索您可從其中匯入的主要資料表格 [!DNL Mixpanel] 至您的 [!DNL Commerce Intelligence] 帳戶。 下清單格將在連線後於您的Data Warehouse中建立 [!DNL Mixpanel]. 若要檢視所有可供追蹤的欄位，請按一下表格名稱欄中的連結。

>[!NOTE]
>
>由於 [!DNL Mixpanel] API、歷史資料 — 從連線日期起七(7)天以前的資料 [!DNL Commerce Intelligence]  — 未復寫。

| **表格名稱** | **說明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表格包含原始事件資料，包括事件、事件日期和平台貯體。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表格包含有關漏斗的資料，包括漏斗ID、漏斗長度（使用者必須完成漏斗的天數）以及漏斗的開始和結束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 這包含來自People Analytics的資料，包括工作階段ID、頁面和使用者資訊，以及上次檢視使用者的日期/時間。 |

{style="table-layout:auto"}

## 相關檔案

* [正在連線 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
