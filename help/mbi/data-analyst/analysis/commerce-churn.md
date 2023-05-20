---
title: 商务流失
description: 了解如何生成和分析您的商务流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# 流失率

本主題說明如何計算 **流失率** 您的 **commerce客戶**. 與SaaS或傳統訂閱公司不同，商務客戶通常沒有具體專案 **&quot;流失事件&quot;** 以向您顯示，他們不應該再指望您的活躍客戶。 因此，下列指示可讓您根據客戶自上次訂購以來經過的確定時間量，將客戶定義為「流失」。

![](../../assets/Churn_rate_image.png)

许多客户在开始时需要获得帮助概念，以了解应根据数据使用哪些 **时间范围** 。 如果要使用历史客户行为定义此 **流失时间范围** ，您可能希望熟悉 [ 定义流失 ](../analysis/define-cust-churn.md) 主题。 然后，您可以在以下说明中使用公式中的结果来获得流失率。

## 计算列

要创建的列

* **`customer_entity`** 表
* **`Customer's last order date`**
   * [!UICONTROL definition]选择：`Max`
   * 选择 [!UICONTROL table] ： `sales_flat_order`
   * 選取 [!UICONTROL column]： `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 選取 [!UICONTROL definition]： `Age`
   * 選取 [!UICONTROL column]： `Customer's last order date`

>[!NOTE]
>
>在构建新报表之前， [ 请确保将所有新列添加为量度 ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 。

## 指标

* **新客户（按首次订购日期）**
   * 计数的客户

>[!NOTE]
>
>此量度可能存在于您的帐户上。

* **`customer_entity`**&#x200B;表格中
* 此量度执行 **计数**
* 於 **`entity_id`** 欄
* 排序依據： **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新客戶（依上次訂購日期）**
   * 计数的客户

   >[!NOTE]
   >
   >此量度可能存在于您的帐户上。

* **`customer_entity`**&#x200B;表格中
* 此量度执行 **计数**
* **`entity_id`**&#x200B;列上
* 按 **`Customer's last order date`** 时间戳排序
* [!UICONTROL Filter]:

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **流失率**
   * [!UICONTROL Metric]：新客戶（依第一筆訂單日期）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 客户上次订购日期后的秒数 > = [ 您自定义的 churned 客户的截止时间&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *量度 `A`：`New customers cumulative`*
* *量度 `B`：`Churned customers by last order date`*
* *量度 `C`：`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

以下是一些常見的月份>秒轉換，但Google提供其他值，包括您可能尋找的任何自訂值的周>秒轉換。

| **月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像上面的範例儀表板。
