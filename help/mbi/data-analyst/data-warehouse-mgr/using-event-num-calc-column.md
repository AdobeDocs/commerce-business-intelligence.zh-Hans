---
title: 事件編號計算欄
description: 瞭解「事件編號」計算欄的用途和用途。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# 事件編號計算欄

本主題概述了 `Event Number` 中可用的計算欄 **[!DNL Manage Data > Data Warehouse]** 頁面。 以下是其功能的說明，隨後是一個範例，以及建立它的機制。

**說明**

此 `Event Number` 欄型別會識別特定事件發生的順序 **事件擁有者**，如 `customer` 或 `user`. 如果您熟悉SQL，則此資料行型別與 `RANK` 函式。 它可用來觀察資料中首次事件、重複事件或第n個事件之間的行為差異。

如果出現連結，此欄會包含相同的 **排名** 對於繫結事件，會略過後續號碼。 例如，如果對數字進行排名5,8，10,10,12，則排名將是1,2，3,3，5。

本欄最常見的使用案例是分析首次購買者和重複購買者。 首次透過新增篩選器（至量度或報表）來識別買家 `Customer's order number` = 1. `Customer's order number` 是型別的欄 `Event Number`.

**範例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上述範例中，欄 `Owner's event number` 是 `Event Number` 欄。 它會根據事件的發生順序(根據 `timestamp` 欄)。

例如，考慮所有列 `owner_id = A`. 表格中的第一列是此擁有者最早的時間戳記，接著是表格中的第三列，接著是表格中的第四列。

**機械**

以下是有關建立 `Event Number` 欄：

1. 導覽至 **[!UICONTROL Manage Data > Data Warehouse]** 頁面。

1. 導覽至您要建立此欄的表格。

1. 按一下 **[!UICONTROL Create a Column]** 並選擇 `EVENT_NUMBER (…)` 欄型別：在 `Same Table` 區段。

1. 第一個下拉式清單 `Event Owner` 指定要決定排名的實體。 若為 `Customer's order number`，客戶識別碼，例如 `customer_id` 或 `customer_email` 會是 `Event Owner`.

1. 第二個下拉式清單 `Event Rank` 指定強制執行決定列排名的順序的欄。 若為 `Customer's order number`，則 `created_at` 時間戳記會是 `Event Rank`.

1. 在 `Options` 下拉式清單中，您可以新增篩選器來排除不予以考慮的列。 排除的列具有 `NULL` 此欄的值。

1. 提供欄的名稱，然後按一下 **[!UICONTROL Save]**.

1. 欄可供使用 _立即。_
