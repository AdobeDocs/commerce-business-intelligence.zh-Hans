---
title: 循序比較計算欄
description: 瞭解「循序比較」計算欄的用途和用法。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 循序比較計算欄

本主題概述了 `Sequential Comparison` 中可用的計算欄 **[!DNL Manage Data > Data Warehouse]** 頁面。 以下是其功能的說明，然後是一個範例和建立它的機制。

**說明**

此 `Sequential Comparison` 欄型別：找出連續事件之間的差異。 最常見的型別 `Sequential Comparison` 欄是 `Seconds since previous order` 欄。 此欄需要三個輸入：

1. `Event Owner`：此輸入決定要將列分組的實體。 例如，在 `Seconds since previous order` 欄位，事件擁有者是客戶，因為您想要尋找自相同客戶的上次訂單開始的秒數。
1. `Event Date`：此輸入會強制執行事件順序。 若為 `Seconds since previous order`，包含訂單時間戳記的欄應為 `Event Date`. 此輸入一律為時間戳記。
1. `Value to Compare`：此輸入為要比較的實際值。 它會從目前列的值減去前一列的值。 因此，系統會呼叫尋找客戶連續訂單之間時間差異的欄 `Seconds since previous order`. 此輸入不一定要是時間戳記。 非時間戳記範例是找出客戶連續訂單之間的訂單值差異。

**範例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

在上述範例中， `Seconds since owner's previous event` 是 `Sequential Comparison` 計算欄。 對於 `owner_id = A`，首先會根據 `timestamp` 欄，然後減去上一個事件的 `timestamp` 從目前事件的時間戳記。 在表格的第三列 — 的第二列 `owner_id A`  — 的值 `Seconds since owner's previous event` 是&#39;2015-01-01 02:00&#39;和&#39;2015-01-01 00之間的秒數:00:00&#39;。 此差異等於兩個小時= 7200秒。

對於此計算欄型別，與擁有者的第一個事件對應的列有 `NULL` 值。

**機械**

若要建立 **事件編號** 欄：

1. 導覽至 **[!DNL Manage Data > Data Warehouse]** 頁面。

1. 導覽至您要建立此欄的表格。

1. 按一下 **[!UICONTROL Create New Column]** 右上角。

1. 選取 `Same Table` 作為 `Definition Type` （如果您要比較的欄不在同一個表格上，您可能需要將它們重新定位）。

1. 選取 `SEQUENTIAL_COMPARISON` 作為 `Column Definition Equation`.

1. 選擇輸入，如上所述：
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 您也可以新增篩選器，以排除不要考慮的列。 排除的列具有 `NULL` 此欄的值。

1. 提供頁面頂端欄的名稱，然後按一下 **[!UICONTROL Save]**.

1. 欄可供使用 *立即*.

![秒](../../assets/SEC_new.png)
