---
title: Commerce流失
description: 瞭解如何產生及分析您的Commerce流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# 流失率

本主題說明如何計算 **流失率** 您的 **commerce客戶**. 與SaaS或傳統訂閱公司不同，商務客戶通常沒有具體專案 **&quot;流失事件&quot;** 以向您顯示，他們不應該再指望您的活躍客戶。 因此，下列指示可讓您根據客戶自上次訂購以來經過的確定時間量，將客戶定義為「流失」。

![](../../assets/Churn_rate_image.png)

許多客戶都希望獲得協助，以開始概念化 **時間範圍** 他們應該根據其資料使用。 如果您想要使用歷史客戶行為來定義此專案 **流失時間範圍**，請熟悉 [定義流失](../analysis/define-cust-churn.md) 主題。 然後，您便可以在以下說明中使用流失率公式中的結果。

## 計算欄

要建立的欄

* **`customer_entity`** 表格
* **`Customer's last order date`**
   * 選取 [!UICONTROL definition]： `Max`
   * 選取 [!UICONTROL table]： `sales_flat_order`
   * 選取 [!UICONTROL column]： `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 選取 [!UICONTROL definition]： `Age`
   * 選取 [!UICONTROL column]： `Customer's last order date`

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 量度

* **新客戶（依第一筆訂單日期）**
   * 被計數的客戶

>[!NOTE]
>
>此量度可能存在於您的帳戶中。

* 在 **`customer_entity`** 表格
* 此量度會執行 **計數**
* 於 **`entity_id`** 欄
* 排序依據： **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新客戶（依上次訂購日期）**
   * 被計數的客戶

   >[!NOTE]
   >
   >此量度可能存在於您的帳戶中。

* 在 **`customer_entity`** 表格
* 此量度會執行 **計數**
* 於 **`entity_id`** 欄
* 排序依據： **`Customer's last order date`** timestamp
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
   * 自客戶上次訂購日期以來的秒數>= [您為流失客戶定義的截止日期&#x200B;]**`^`**
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
