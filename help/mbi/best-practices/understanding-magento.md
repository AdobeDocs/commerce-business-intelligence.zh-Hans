---
title: 瞭解您的 [!DNL Commerce Intelligence] 環境
description: 瞭解如何使用並改善您的 [!DNL Commerce Intelligence] 環境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# 您的 [!DNL Adobe Commerce Intelligence] 環境

分析商務資料時，請注意這些因素和常見的誤解。 如果您需要協助以確保正確使用您的Commerce結構描述，請立即 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

許多表格包含名為的欄 `entity\_id`. 在每個包含 `entity\_id`，該欄用於識別唯一列。

例如， `sales\_order` 表格為唯一順序。 此表格中的主索引鍵稱為 `entity\_id`. 可將此欄視為 `order\_id`. 在另一個表格中， `customer\_entity`，每一列代表一個不重複客戶。 此表格中的主索引鍵也稱為 `entity\_id`，這可以視為 `customer\_id`.

在這些表格中， `sales\_order.entity\_id` 不等於 `customer\_entity.entity\_id`. 這適用於包含下列專案的所有資料表集： true `entity\_id`： `table\_A.entity\_id` 不等於 `table\_B.entity\_id`.

## [!DNL Guest orders]

如果您允許客戶在沒有帳戶的情況下從您的網站訂購（訪客訂單），這些客戶不會將填入為 `customer\_entity` 表格。 此外，訪客下單的每個訂單都有一個Null `customer\_id` 上的值 `sales\_order` 表格。

因此，如果您想要追蹤來賓在一段時間內的行為，所有客戶層級欄位都必須在頁面上計算 `sales\_order` 表格，使用客戶識別碼，例如 `customer\_email`.

如果您使用 `sales\_order` 表格作為客戶表格時，您建立客戶層級量度時必須小心。 例如，考慮平均期限收入量度。 此量度用於識別客戶群中的平均期限收入。 首先，需要新欄，讓每個客戶傳回其期限收入。 接著，您必須平均此欄位才能取得客戶的平均期限收入。

如果您能使用 `customer\_entity` 表格中，每一列都是單一客戶，且每個客戶僅存在於該表格中一次。 因此，當您有期限收入欄時，您只需要建立平均量度即可。 不過，如果您使用 `sales\_order` 表格作為您的客戶表格，客戶可能會存在於許多列中。 設定期限收入欄後，指定客戶下的每個訂單（列）會顯示客戶的期限收入；但您只想將該客戶納入整體平均量度一次。

這裡的訣竅在於您必須將篩選器新增至量度，確保只包含每位客戶一次。 Adobe鼓勵您建立並使用篩選器集，命名為 **我們計算的客戶** 篩選條件 **客戶的訂單編號= 1** （您可能需要使用其他篩選器來排除不想要的客戶）。 新增此篩選器可確保您將每個客戶僅納入客戶層級量度一次。

## 產品和類別

產品可以有多個類別，而類別可用於多個產品。 因此，在設定類別層級分析時，您必須小心使用正確的定義。 您要頂層類別嗎？ 第二層類別？ 如果產品可能屬於多個頂層類別，該怎麼辦？

想像一下，根據Commerce實作的定義，有一對牛仔褲分為3個不同的類別層級：「服飾」（頂層）、「外套」（第二層）和「褲子」（第三層）。 您可能希望依售出件數來分析類別效能。 此分析所需的量度為 _已售出專案_，建立在 `sales\_order\_item` 表格。 因此，您必須將類別層級資訊移至料號表格。 上的每一列 `sales\_order\_item` 表格具有相關聯的 `product\_id`，因此，如果您知道與產品相關聯的類別，則可將該資訊移至所需的表格。

在移動任何資料之前，您必須先知道適當的聯結和篩選器，以確保您擷取正確的類別。 對於某些分析，您可能需要知道「褲子」，但在其他分析中，「服裝」可能更合適。 這些是需個別識別的相異類別。 瞭解每個分類層次如何定義，可確保您將單位銷售歸因到適合您特定分析的類別。

現在，假設您也有一個 `Our Favorites` 網站首頁上的最上層類別。 您可能已實作Commerce商店，將Jean納入 `Clothing` 類別與 `Our Favorites` 類別。 如果是這樣的話，這雙牛仔褲會有多個頂層類別。 在這種情況下，請將單一頂層類別移至 `sales\_order\_item` 表格並不完全合理，因為有多種選項。 若要解決此問題，Adobe建議建立檢查特定類別的是/否欄。 例如， `Is product in Clothing category?` 和 `Is product in Our Favorites category?` 欄可讓您檢查產品是否屬於這些特定類別。
