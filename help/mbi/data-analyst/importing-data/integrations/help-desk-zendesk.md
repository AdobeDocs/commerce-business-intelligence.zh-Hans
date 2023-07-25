---
title: Zendesk技术支持报告
description: 了解您最宝贵的推荐渠道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 技术支持报告 [!DNL Zendesk]

>[!NOTE]
>
>这仅适用于位于以下位置的客户端： `Pro` 规划并使用新架构。 如果您拥有以下优势，那么您将使用新架构： `Data Warehouse Views` 部分在选择后可用 `Manage Data` 从主工具栏中。

整合您的 [!DNL Zendesk] 使用事务型数据库的数据是更好地了解客户如何与销售或客户成功团队进行交互的绝佳方法。 它还有助于您了解哪些类型的客户在使用您的支持平台。 本主题演示如何设置功能板以获取有关您的产品的详细报告 [!DNL Zendesk] 性能，以及您的事务型客户的关系。

在开始之前，您想要连接 [[!DNL Zendesk]](../integrations/zendesk.md). 此分析包含 [高级计算列](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## 快速入门

### 要跟踪的列

* `audits` 表
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 表
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 表
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 表
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要创建的筛选器集

* `[!DNL Zendesk] Tickets` 表
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 计算列

### 要创建的列

* **`[!DNL Zendesk] user's`** 表
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `答！=`end-user` 则 `Yes` 时间 `B` 不是 `null` 和 `B` 点赞 `%@magento.com` 则 `Yes` else `No` 结束

      * Replace `@magento.com` 使用您的域

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** 表
   * 选择定义： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 选择 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择 [!UICONTROL column]： `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** 表
   * 选择定义： `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * 选择 [!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 选择定义： `Exists`
   * 选择 [!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** 表
   * 选择定义： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 选择 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择 [!UICONTROL column]： `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 选择定义： `Joined Column`
   * 选择 [!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择 [!UICONTROL column]： `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 选择定义： `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * 选择 [!UICONTROL table]： `[!DNL Zendesk] audits`
   * 选择 [!UICONTROL column]： `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` 已更改为 `solved = 1`

   * 选择定义： `Min`
   * 选择 [!UICONTROL table]： `[!DNL Zendesk] audits`
   * 选择 [!UICONTROL column]： `created_at`
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

      * `Ticket's latest solved date` 减号 `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` 减号 `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type`  — “相同表>计算”

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype`  — 整数

* **`Ticket created_at (day of week)`**
   * 
      * `Column type`  — “相同表>计算”

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` – `String`

* **`customer_entity`** 表
   * 选择定义： `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [！UICONTROL One]: `customer_entity.email`

   * 选择 [!UICONTROL table]： `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type`  — “相同表>计算”

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** 表
   * 选择定义： `Joined Column`
   * 选择 [!UICONTROL table]： `customer_entity`
   * 选择 [!UICONTROL column]： `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 量度

* **[!DNL Zendesk]新票证**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此量度执行 **计数**
* 在 **`id`** 列
* 排序依据 **`created_at`** 时间戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]已解决票证**
   * `Tickets we count`
   * 中的状态 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此量度执行 **计数**
* 在 **`id`** 列
* 排序依据 **`created_at`** 时间戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]不同的用户提交票证**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此量度执行 **非重复计数**
* 在 **`requester_id`** 列
* 排序依据 **`created_at`** 时间戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/中间票证解析时间**
   * `Tickets we count`
   * 中的状态 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此量度执行 **平均值（或中间值）**
* 在 **`Seconds to resolution`** 列
* 排序依据 **`created_at`** 时间戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]首次响应的平均时间/中位数**
   * 已计票的票证
   * 状态为关闭，已解决

* 在 **`[!DNL Zendesk] tickets`** 表
* 此量度执行 **平均值（或中间值）**
* 在 **`Seconds to first response`** 列
* 排序依据 **`created_at`** 时间戳
* [!UICONTROL Filter]:

>[!NOTE]
>
>确保 [将所有新列作为维度添加到量度](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。

### 报告

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 中的状态 `new, open, pending`

* 量度 `A`： `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 中的状态 `solved, closed`

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
   * 中的状态 `solved, closed`

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
   * 中的状态 `solved, closed`

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
     [！UICONTROL量度]: Users

* 量度 `A`： `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
