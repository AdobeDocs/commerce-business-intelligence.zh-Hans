---
title: Zendesk服務檯報告
description: 瞭解您最重視的轉介管道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 服務檯報告 [!DNL Zendesk]

>[!NOTE]
>
>這僅適用於位於「 」的使用者端。 `Pro` 規劃並使用新架構。 如果您擁有以下優勢，即可使用新架構： `Data Warehouse Views` 選取後可用的區段 `Manage Data` 從主工具列。

整合您的 [!DNL Zendesk] 透過交易式資料庫取得資料，是您深入瞭解客戶與銷售或客戶成功團隊互動情況的絕佳方式。 它還有助於您瞭解哪些型別的客戶正在使用您的支援平台。 本主題示範如何設定控制面板，以取得與您的網站相關的精細報表。 [!DNL Zendesk] 交易式客戶的效能和時間。

開始之前，您想要連線 [[!DNL Zendesk]](../integrations/zendesk.md). 此分析包含 [進階計算欄](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## 快速入門

### 要追蹤的欄

* `audits` 表格
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 表格
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 表格
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 表格
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要建立的篩選器集

* `[!DNL Zendesk] Tickets` 表格
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 計算欄

### 要建立的欄

* **`[!DNL Zendesk] user's`** 表格
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `答！=`end-user` 則 `Yes` 時間 `B` 不是 `null` 和 `B` 按讚 `%@magento.com` 則 `Yes` 否則 `No` 結束

      * Replace `@magento.com` 與您的網域

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** 表格
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 選取 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取 [!UICONTROL column]： `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** 表格
   * 選取定義： `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * 選取 [!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 選取定義： `Exists`
   * 選取 [!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** 表格
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 選取 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取 [!UICONTROL column]： `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取 [!UICONTROL column]： `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選取定義： `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * 選取 [!UICONTROL table]： `[!DNL Zendesk] audits`
   * 選取 [!UICONTROL column]： `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` 已變更為 `solved = 1`

   * 選取定義： `Min`
   * 選取 [!UICONTROL table]： `[!DNL Zendesk] audits`
   * 選取 [!UICONTROL column]： `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` 減號 `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` 減號 `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type`  — 「相同表格>計算」

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype`  — 整數

* **`Ticket created_at (day of week)`**
   * 
      * `Column type`  — 「相同表格>計算」

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` – `String`


* **`customer_entity`** 表格
   * 選取定義： `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 

      [！UICONTROL One]: `customer_entity.email`

   * 選取 [!UICONTROL table]： `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type`  — 「相同表格>計算」

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** 表格
   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]： `customer_entity`
   * 選取 [!UICONTROL column]： `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 量度

* **[!DNL Zendesk]新票證**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表格
* 此量度會執行 **計數**
* 於 **`id`** 欄
* 排序依據： **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]已解決的票證**
   * `Tickets we count`
   * 中的狀態 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表格
* 此量度會執行 **計數**
* 於 **`id`** 欄
* 排序依據： **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]不同的使用者提交票證**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表格
* 此量度會執行 **相異計數**
* 於 **`requester_id`** 欄
* 排序依據： **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/中位票證解析時間**
   * `Tickets we count`
   * 中的狀態 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表格
* 此量度會執行 **平均（或中位數）**
* 於 **`Seconds to resolution`** 欄
* 排序依據： **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]首次回應的平均/中位時間**
   * 已計票的票證
   * 狀態為關閉，已解決

* 在 **`[!DNL Zendesk] tickets`** 表格
* 此量度會執行 **平均（或中位數）**
* 於 **`Seconds to first response`** 欄
* 排序依據： **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

### 報表

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 中的狀態 `new, open, pending`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 中的狀態 `solved, closed`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 量度 `A`： `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 中的狀態 `solved, closed`

* 量度 `A`： `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`： `New tickets`
* 量度 `B`： `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 量度 `A`： `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 中的狀態 `solved, closed`

* 量度 `A`： `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 量度 `A`： `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 量度 `A`： `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [！UICONTROL公制]: Users

* 量度 `A`： `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
