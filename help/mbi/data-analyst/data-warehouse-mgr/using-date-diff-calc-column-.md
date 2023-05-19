---
title: 使用日期差異計算欄
description: 瞭解日期差異計算欄的用途和用途。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 日期差異計算欄

本主題概述了 `Date Difference` 中可用的計算欄 **[!DNL Manage Data > Data Warehouse]** 頁面。 以下是其功能的說明，隨後是一個範例，以及建立它的機制。

**說明**

此 `Date Difference` column type會根據事件時間戳記，計算屬於單一記錄之兩個事件之間的時間。 此欄中計算的原始值以秒為單位，但會自動轉換為分鐘、小時、天等值，以便顯示在報表中。 不過，當您作為篩選/群組使用時，您想要以秒為單位使用該值。

A `date difference` 「計算」欄可用來建立量度，以計算兩個事件之間的平均或中間時間，例如客戶註冊與其第一筆訂單之間的平均時間。

**範例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


在上述範例中， `Date Difference` 欄是 `Seconds between timestamp_2 and timestamp_1` 欄。 它會執行計算 `timestamp_2 minus timestamp_1`.

**機械**

下列步驟說明如何建立 `Date Difference` 欄。

1. 導覽至 **[!DNL Manage Data > Data Warehouse]** 頁面。
1. 導覽至您要建立此欄的表格。
1. 按一下 **[!UICONTROL Create a Column]** 並依照以下方式設定您的欄：
   * 選取 `Column Definition Type` > `Same Table`
   * 選取 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 選取 `Ending DATETIME` 欄>選擇結束日期時間欄位，這通常是稍後發生的事件
   * 選取 `Starting DATETIME` column** >選擇開始日期時間欄位，這通常是較早發生的事件

1. 為欄命名，然後按一下 **[!UICONTROL Save]**.
1. 欄可供使用 *立即*.

例如，下列範例設定為計算 `Seconds between order date and customer's creation date`：

![](../../assets/date_diff.png)
