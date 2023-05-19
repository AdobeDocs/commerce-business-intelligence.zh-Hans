---
title: 瞭解資料庫和SQL編輯器之間的結果
description: 瞭解瞭解資料庫和SQL編輯器之間的結果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 資料庫結果vs [!DNL SQL Editor] 結果

您可能會好奇 `Last successful update began` 欄位位於您的 `Integrations` 頁面：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 瞭解 `timestamp` 欄位

它會顯示開始 `timestamp` （在您帳戶上設定的時區內） _上次成功更新週期_ 在您的帳戶上。

- 如果任何已同步表格在上次更新週期期間發生問題，則此時間戳記為 *未更新*.
- 因此，在某些情況下，報表可能已更新為全新資料，但 *上次成功更新已開始* 仍落後。

## 識別「真正的」最後一個資料點

特定整合的最新資料點由 `Last Data Point Received` 時間戳記，位於每個整合的右側。 該時間戳記指您的Data Warehouse成功從該來源接收資料點的最後一個時間，無論該來源是資料庫、API或第三方整合。

檢查資料的時效性 *特定表格*，Adobe建議快速建立 [[!DNL SQL] 報告](../../dev-reports/sql-rpt-bldr.md) 會執行 `MAX(timestamp)` 在您帳戶的最重要表格上。 將此時間戳記與 `Last Data Point` 指出問題是否影響整個帳戶或表格子集。 Adobe建議對三至四個重要、常用的表格執行此動作。

- 如果 `MAX(timestamp)` 值晚於 `Last Data Point Received`，這表示一部分表格受到影響，但整體帳戶的更新週期穩定。
- 如果 `MAX(timestamp)` 值等於或早於 `Last Data Point Received`，這表示帳戶的更新週期受到影響。 在此情況下， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
