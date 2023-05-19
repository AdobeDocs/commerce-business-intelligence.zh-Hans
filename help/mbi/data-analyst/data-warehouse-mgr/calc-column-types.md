---
title: 計算欄型別
description: 瞭解如何建立欄，以擴充和最佳化您的資料進行分析。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 計算欄型別

* [相同的表格計算](#sametable)
* [一對多計算](#onetomany)
* [多對一計算](#manytoone)
* [便利的參考地圖](#map)
* [進階計算欄](#advanced)

在內 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)，您可以建立欄，以擴充和最佳化資料進行分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 選取「Data Warehouse管理員」中的任何表格，然後按一下 **[!UICONTROL Create New Column]**.

本主題說明您可以使用「Data Warehouse管理員」建立的欄型別。 此外也涵蓋說明、該欄的視覺化逐步解說，以及 [參考地圖](#map) 建立欄所需的所有輸入。 建立計算欄有三種方式：

1. [相同的表格計算資料行](#sametable)
1. [一對多計算欄](#onetomany)
1. [多對一計算欄](#manytoone)

## 相同的表格計算資料行 {#sametable}

這些資料欄是使用來自相同表格的輸入資料欄建置。

### 年齡 {#age}

期限計算欄會傳回目前時間與某個輸入時間之間的秒數。

以下範例會建立 `Seconds since customer's most recent order` 在 `customers` 表格。 這可用來建構尚未在中進行購買（有時稱為流失）的客戶的使用者清單 `X days`.

![](../../assets/age.gif)

### 貨幣轉換器

貨幣轉換器計算欄將欄的原生貨幣轉換為所需的新貨幣。

以下範例會建立 `base\_grand\_total In AED`，轉換 `base\_grand\_total` 從原生貨幣到AED (在 `sales\_flat\_order` 表格。 此欄適用於擁有多種貨幣，且想以當地貨幣報告的商店。

對於Commerce使用者端， `base\_currency\_code` 欄位通常會儲存原生貨幣。 此 `Spot Time` 欄位應符合量度中使用的日期。

![](../../assets/currency_converter.png)

## 一對多計算欄 {#onetomany}

`One-to-Many` 欄 [使用兩個表格之間的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 此路徑一律代表一個表格，其中有一個屬性存在；以及多個表格，其中屬性會向下被「重新定位」。 路徑可描述為 `foreign key--primary key` 關係。

### 聯結欄 {#joined}

聯結欄會重新定位一個表格上的屬性 *至* 多張表格。 一個/多個的典型範例是客戶（一個）和訂單（多個）。

在以下範例中， `Customer's group\_id` 維度向下連結至 `orders` 表格。

![](../../assets/joined_column.gif)

## 多對一計算欄 {#manytoone}

這些欄使用與一對多欄相同的路徑，但它們將資料指向相反的方向。 欄會建立在路徑的一側，而不是多側。 由於這種關係，欄中的值必須是彙總，也就是說，對許多側的資料點執行的數學運算。 這方面的使用案例有很多，下面列出了一些案例。

### 計數 {#count}

此型別的計算欄會傳回許多資料表上的值計數 *onto* 一個表格。

在以下範例中，維度 `Customer's lifetime number of canceled orders` 建立於 `customers` 表格(具有篩選器 `orders.status`)。

![](../../assets/many_to_one.gif){： width=&quot;699&quot; height=&quot;351&quot;}

### 總和 {#sum}

「總和」計算欄是 `many` 將表格移至單一表格。

這可用來建立客戶層級的維度，例如 `Customer's lifetime revenue`.

### 最小值或最大值 {#minmax}

最小值或最大值計算欄會傳回多面存在的最小或最大記錄。

這可用來建立客戶層級的維度，例如 `Customer's first order date`.

### 存在 {#exists}

計算欄是判斷在多面是否存在記錄的二進位測試。 換言之，新欄會傳回 `1` 如果路徑連線每個表格中的至少一列，並且 `0` 如果無法建立連線。

例如，此型別的維度可能決定客戶是否購買過特定產品。 使用a之間的聯結 `customers` 表格和 `orders` 表格、特定產品的篩選器、維度 `Customer has purchased Product X?` 可以建置。

## 便利的參考地圖 {#map}

如果您在建立計算欄時遇到無法記住所有輸入內容的問題，請在建立時將此參考地圖備妥使用：

![](../../assets/merged_reference_map.png)

## 進階計算欄 {#advanced}

當您想要分析和回答有關您業務的問題時，可能會遇到無法建立所需確切欄的情況。

為確保快速週轉，Adobe建議將 [進階計算欄型別](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南以瞭解Adobe支援團隊可建立哪種欄。 該主題也涵蓋您建立欄所需的資訊 — 將其包含在您的請求中。

## 相關檔案

* [建立計算欄](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [建立/刪除計算欄的路徑](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [瞭解和評估表格關係](../../data-analyst/data-warehouse-mgr/table-relationships.md)
