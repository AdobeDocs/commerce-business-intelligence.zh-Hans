---
title: 來賓訂單
description: 瞭解訪客訂單對您資料的影響，以及您對於訪客訂單必須正確考慮哪些選項。 [!DNL Commerce Intelligence] Data Warehouse。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 來賓訂單

複查訂單時，如果您注意到訂單數量過多 `customer\_id` 值為null或沒有值可聯結回 `customers` 表格，這表示您的商店允許訪客訂購。 這表示您的 `customers` 表格很可能並未包含您的所有客戶。

本主題討論訪客訂單對您資料的影響，以及您對於貴公司中的訪客訂單必須正確考慮哪些選項。 [!DNL Commerce Intelligence] Data Warehouse。

## 訪客訂單對資料的影響

在典型的商務資料庫中， `orders` 聯結至的表格 `customers` 表格。 上的每一列 `orders` 表格具有 `customer\_id` 欄中唯一的一列 `customers` 表格。

* **如果所有客戶都已註冊** 而且不允許客服訂單，這表示 `orders` 表格中有一個 `customer\_id` 欄。 因此，每個訂單都會聯結回 `customers` 表格。

   ![](../../assets/guest-orders-4.png)

* **如果允許來賓訂單**，這表示有些訂單在 `customer\_id` 欄。 只有註冊客戶會獲指定的 `customer\_id` 上的欄 `orders` 表格。 未註冊的客戶會收到 `NULL` （或空白）值。 因此，並非所有訂單記錄在 `customers` 表格。

   >[!NOTE]
   >
   >若要識別發出訂單的唯一個人，必須在旁邊有另一個唯一的使用者屬性 `customer\_id` 附加至訂單。 通常會使用客戶的電子郵件地址。

## 如何在Data Warehouse設定中說明來賓訂單

通常，實作您的帳戶的銷售工程師會在建立Data Warehouse基礎時考慮來賓訂單。

說明訪客訂單的最佳方式是，將所有客戶層級量度建立在 `orders` 表格。 此設定使用所有客戶擁有的唯一客戶ID，包括來賓（通常使用客戶電子郵件）。 這會忽略以下專案的註冊資料： `customers` 表格。 使用此選項時，客戶層級報表中只會包含已購買至少一次的客戶。 尚未購買一次的註冊使用者不包括在內。 透過此選項，您的 `New customer` 量度是根據客戶在「 」中的首次訂購日期 `orders` 表格。

您可能會注意到 `Customers we count` 在此型別設定中設定的篩選具有的篩選器 `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

在沒有訪客訂單的情況下，每個客戶在客戶表格中都會以不重複資料列存在（請參閱圖1）。 量度，例如 `New customers` 只需根據下列條件計算此表格的id `created\_at` 根據註冊日期瞭解新客戶的日期。

在客體訂單設定中，所有客戶量度均以 `orders` 若要說明來賓訂單，您必須確定 `not counting customers twice`. 如果您計算訂單表格的ID，則會計算每個訂單。 如果您改為計算ID `orders` 表格並使用篩選器， `Customer's order number = 1`，則您將會計算每個不重複客戶 `only one time`. 這適用於所有客戶層級量度，例如 `Customer's lifetime revenue` 或 `Customer's lifetime number of orders`.

您可以在上方看到有null `customer\_ids` 在 `orders` 表格。 如果您使用 `customer\_email` 若要識別獨特客戶，您可以看到 `erin@test.com` 已下三(3)份訂單。 因此，您可以建置 `New customers` 量度在您的 `orders` 資料表，其條件如下：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
