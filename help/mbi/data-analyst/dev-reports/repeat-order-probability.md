---
title: 重複訂購機率報表
description: 瞭解並瞭解「重複訂購機率」報表。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 重複訂購機率報表

## 何時為 `Incremental Event Probability` 有透視可用嗎？

此 `incremental event probability` 「透視」僅適用於篩選器使用對所有訂單都相等的維度(例如，使用者的 `gender`，使用者的 `age` 或使用者的 `source`)。

這是因為此觀點仰賴一個名為的維度 `User's order number` 區段劃分，計算使用者的購買數（例如，John的第一次、第二次和第三次訂單）。

如果您新增的篩選使用並非對所有訂單都相等的維度(例如， `Order's Region`)， `User's order number` 維度將不再準確。 這是因為在為使用者的訂單編號時，並未考慮特定區域（例如，John的第1、第2、第3筆訂單仍相同，無論其區域為何）。

## 將訂單特定維度轉換為使用者特定維度

在某些情況下，您或許可以將 `order-specific` 將維度移入 `user-specific` 要新增為篩選器的維度 `Repeat Order Probability` 圖表。 在這些情況下，您會傳回使用者第一個訂單或最新訂單的訂單屬性（例如，使用者的第一個訂單區域名稱）。

如果您想要建立此類新維度， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 比較不同屬性的訂單重複機率

若要比較不同訂單屬性(例如訂單的 `region`)，Adobe建議建立類似以下的圖表 `Users by lifetime number of orders`. 這會顯示產生1、2、3...期限訂單數並新增訂單層級篩選器的使用者人數。 （換言之，這可顯示使用者是否在一個地區或另一個地區進行多次重複購買。）

組成此類圖表的數字可匯出至Excel以計算重複順序機率比率。 若要檢視客戶進行下列活動的機率： `(x)` 要完成的訂單 `(x+1)` 訂購，簡單` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 購買。

### 範例：

| 類別 | 值 |
|---|---|
| 一生中購買1次的客戶數 | `90` |
| 一生中購買2次的客戶數 | `30` |
| 一生中購買3次的客戶數 | `10` |
| 已在其一生中購買過一次以再次購買的客戶的重複訂購機率 | `(30 + 10) / (30+10+90) = 30.77%` |
