---
title: Zendesk技术支持报告
description: 了解您最宝贵的转介渠道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# [!DNL Zendesk]的技术支持报告

>[!NOTE]
>
>这仅适用于`Pro`计划上且使用新架构的客户端。 如果您在主工具栏中选择`Manage Data`后有`Data Warehouse Views`部分可用，则表示您使用的是新架构。

将[!DNL Zendesk]数据与事务数据库整合是更好地了解客户如何与您的销售或客户成功团队进行交互的绝佳方法。 它还有助于您了解哪些类型的客户在使用您的支持平台。 本主题演示如何设置功能板，以获取有关[!DNL Zendesk]性能以及事务型客户关联情况的精细报告。

在开始之前，您要连接[[!DNL Zendesk]](../integrations/zendesk.md)。 此分析包含[高级计算列](../../data-warehouse-mgr/adv-calc-columns.md)。

<!-- Getting Started -->

## 快速入门

### 要跟踪的列

* `audits`表
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events`表
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets`表
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users`表
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要创建的筛选器集

* `[!DNL Zendesk] Tickets`表
   * `status != deleted`

* `Filter set name`： `Tickets we count`
* `Filter set logic`：

## 计算列

### 要创建的列

* **`[!DNL Zendesk] user's`**&#x200B;表
   * `User is agent? (Yes/No) `
   * &#x200B;
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`，`email`

      * `SQL Calculation` `- case when `A` is not `null` and `A！=`end-user`然后`Yes`，当`B`不是`null`并且`B`如`%@magento.com`然后`Yes`否则`No`结束

      * 将`@magento.com`替换为您的域

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`**&#x200B;表
   * 选择定义： `Joined Column`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]： `[!DNL Zendesk] users.id`

   * 选择[!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择[!UICONTROL column]： `User is agent? (Yes/No)`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`**&#x200B;表
   * 选择定义： `Exists`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]： `[!DNL Zendesk] audits._id`

   * 选择[!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]：
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 选择定义： `Exists`
   * 选择[!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]： `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`**&#x200B;表
   * 选择定义： `Joined Column`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]： `[!DNL Zendesk] users.id`

   * 选择[!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择[!UICONTROL column]： `email`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 选择定义： `Joined Column`
   * 选择[!UICONTROL table]： `[!DNL Zendesk] users`
   * 选择[!UICONTROL column]： `role`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 选择定义： `Max`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]： `[!DNL Zendesk] tickets.id`

   * 选择[!UICONTROL table]： `[!DNL Zendesk] audits`
   * 选择[!UICONTROL column]： `created_at`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]：
   * `status`已更改为`solved = 1`

   * 选择定义： `Min`
   * 选择[!UICONTROL table]： `[!DNL Zendesk] audits`
   * 选择[!UICONTROL column]： `created_at`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]：
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date`减去`created_at`

* **`Seconds to first response`**
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date`减去`created_at`

* **`Requester's ticket number`**
   * &#x200B;
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * &#x200B;
      * `Column type` — “相同表>计算”

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` — 整数

* **`Ticket created_at (day of week)`**
   * &#x200B;
      * `Column type` — “相同表>计算”

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`**&#x200B;表
   * 选择定义： `Count`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] tickets.email`
   * &#x200B;

     [!UICONTROL One]: `customer_entity.email`

   * 选择[!UICONTROL table]： `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]：
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * &#x200B;
      * `Column type` — “相同表>计算”

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`**&#x200B;表
   * 选择定义： `Joined Column`
   * 选择[!UICONTROL table]： `customer_entity`
   * 选择[!UICONTROL column]： `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 量度

* **[!DNL Zendesk]张新票证**
   * `Tickets we count`

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;表中
* 此量度执行&#x200B;**计数**
* 在&#x200B;**`id`**&#x200B;列上
* 按&#x200B;**`created_at`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]个已解决的票证**
   * `Tickets we count`
   * `closed, solved`中的状态

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;表中
* 此量度执行&#x200B;**计数**
* 在&#x200B;**`id`**&#x200B;列上
* 按&#x200B;**`created_at`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]个不同的用户归档票证**
   * `Tickets we count`

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;表中
* 此量度执行&#x200B;**非重复计数**
* 在&#x200B;**`requester_id`**&#x200B;列上
* 按&#x200B;**`created_at`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]平均/中值票证解析时间**
   * `Tickets we count`
   * `closed, solved`中的状态

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;表中
* 此量度执行&#x200B;**平均值（或中间值）**
* 在&#x200B;**`Seconds to resolution`**&#x200B;列上
* 按&#x200B;**`created_at`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]首次响应的平均/中间时间**
   * 已计票的票证
   * 状态为关闭，已解决

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;表中
* 此量度执行&#x200B;**平均值（或中间值）**
* 在&#x200B;**`Seconds to first response`**&#x200B;列上
* 按&#x200B;**`created_at`**&#x200B;时间戳排序
* [!UICONTROL Filter]：

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)。

### 报告

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]： `New Tickets`
   * [!UICONTROL Filter]：
   * `new, open, pending`中的状态

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]： `New Tickets`
   * [!UICONTROL Filter]：
   * `solved, closed`中的状态

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]： `Average time to first response`

* 量度`A`： `Average time to first response`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]： `Average time to resolution`
   * [!UICONTROL Filter]：
   * `solved, closed`中的状态

* 量度`A`： `Average time to resolution`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `status`
* `Chart Type`： `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]： `New Tickets`

   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* 量度`B`： `Solved tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]： `Average time to first response`

* 量度`A`： `Average time to first response`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]： `Average time to resolution`
   * [!UICONTROL Filter]：
   * `solved, closed`中的状态

* 量度`A`： `Average time to resolution`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]： `Distinct users filing tickets`

* 量度`A`： `Distinct users filing tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Group by`： `Ticket created_at (day of week)`
* `Chart Type`： `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]：`New Tickets`

   * `Show top/bottom`： `Top 100% sorted by created_at (hour of the day)`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Group by`： `Ticket created_at (hour of the day)`
* `Chart Type`： `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]： `Average lifetime revenue`

* 量度`A`： `Average lifetime revenue`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `User has filed a support ticket?`
* `Chart Type`： `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * &#x200B;

     [!UICONTROL 量度]: Users

* 量度`A`： `New users`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `User has filed a support ticket?`
* `Chart Type`： `Column`
