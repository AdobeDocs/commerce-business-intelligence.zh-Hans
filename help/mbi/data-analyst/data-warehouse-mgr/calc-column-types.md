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
* [一对多计算](#onetomany)
* [多對一計算](#manytoone)
* [便利的參考地圖](#map)
* [進階計算欄](#advanced)

在內 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md)，您可以建立欄，以擴充和最佳化資料進行分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 選取「Data Warehouse管理員」中的任何表格，然後按一下 **[!UICONTROL Create New Column]**.

本主題說明您可以使用「Data Warehouse管理員」建立的欄型別。 此外也涵蓋說明、該欄的視覺化逐步解說，以及 [參考地圖](#map) 建立欄所需的所有輸入。 创建计算列的方法有三种：

1. [相同的表格計算資料行](#sametable)
1. [一對多計算欄](#onetomany)
1. [多對一計算欄](#manytoone)

## 相同的表格計算資料行 {#sametable}

这些列是使用同一表中的输入列生成的。

### 年龄 {#age}

年龄计算列返回当前时间与某些输入时间之间的秒数。

下面的示例在表格中 `customers` 创建 `Seconds since customer's most recent order` 。可用于构建未在中 `X days` 进行购买的客户用户列表（有时也称为 churning）。

![](../../assets/age.gif)

### 货币转换器

貨幣轉換器計算欄將欄的原生貨幣轉換為所需的新貨幣。

以下範例會建立 `base\_grand\_total In AED`，轉換 `base\_grand\_total` 從原生貨幣到AED (在 `sales\_flat\_order` 表格。 此欄適用於擁有多種貨幣，且想以當地貨幣報告的商店。

對於Commerce使用者端， `base\_currency\_code` 欄位通常會儲存原生貨幣。 此 `Spot Time` 欄位應符合量度中使用的日期。

![](../../assets/currency_converter.png)

## 一对多计算列 {#onetomany}

`One-to-Many` 列 [ 使用两个表 ](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 之间的路径。 此路徑一律代表一個表格，其中有一個屬性存在；以及多個表格，其中屬性會向下被「重新定位」。 路徑可描述為 `foreign key--primary key` 關係。

### 聯結欄 {#joined}

聯結欄會重新定位一個表格上的屬性 *至* 多張表格。 一個/多個的典型範例是客戶（一個）和訂單（多個）。

在以下範例中， `Customer's group\_id` 維度向下連結至 `orders` 表格。

![](../../assets/joined_column.gif)

## 多對一計算欄 {#manytoone}

这些列使用与一对多列相同的路径，但它们以相反的方向指向数据。 欄會建立在路徑的一側，而不是多側。 由於這種關係，欄中的值必須是彙總，也就是說，對許多側的資料點執行的數學運算。 這方面的使用案例有很多，下面列出了一些案例。

### 計數 {#count}

此型別的計算欄會傳回許多資料表上的值計數 *onto* 一個表格。

在以下範例中，維度 `Customer's lifetime number of canceled orders` 建立於 `customers` 表格(具有篩選器 `orders.status`)。

![](../../assets/many_to_one.gif){： width = &quot;699&quot; height = &quot;351&quot;}

### 和 {#sum}

计算列总和是表格中 `many` 值与一个表格的总和。

这可用于创建客户级维度点赞 `Customer's lifetime revenue` 。

### 最小或最大 {#minmax}

最小值或最大值計算欄會傳回多面存在的最小或最大記錄。

這可用來建立客戶層級的維度，例如 `Customer's first order date`.

### 存在 {#exists}

计算列是一个二进制测试，用于确定记录在多个侧是否存在。 换句话说，如果路径至少连接了每个表中的一行，并且 `0` 无法建立连接，则新列将返回 a `1` 。

例如，如果客户曾购买了特定产品，则此类维度可能会决定。 使用表和 `orders` 表之间 `customers` 的联接、特定产品的过滤器，可以建立维度 `Customer has purchased Product X?` 。

## 方便的参考图 {#map}

如果您在建立計算欄時遇到無法記住所有輸入內容的問題，請在建立時將此參考地圖備妥使用：

![](../../assets/merged_reference_map.png)

## 進階計算欄 {#advanced}

當您想要分析和回答有關您業務的問題時，可能會遇到無法建立所需確切欄的情況。

為確保快速週轉，Adobe建議將 [進階計算欄型別](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南以瞭解Adobe支援團隊可建立哪種欄。 該主題也涵蓋您建立欄所需的資訊 — 將其包含在您的請求中。

## 相关文档

* [创建计算列](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [创建/删除计算列的路径](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [了解和评估表关系](../../data-analyst/data-warehouse-mgr/table-relationships.md)
