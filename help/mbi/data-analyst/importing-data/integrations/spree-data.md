---
title: 預期的Spree資料
description: 探索可從Spree匯入的主要資料表 [!DNL Commerce Intelligence] 帳戶。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 預期 [!DNL Spree] 資料

在您擁有 [已連線您的 [!DNL Spree] 儲存](../../../data-analyst/importing-data/integrations/spree.md)，您可以使用 [Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤您網站上的 [!DNL Spree] 分析平台。

本主題會探索您可從其中匯入的主要資料表格 [!DNL Spree] 至您的 [!DNL Commerce Intelligence] 帳戶，包括連結 [其他檔案](https://guides.spreecommerce.org/developer/addresses.html#address) 關於 [!DNL Spree] 資料。

| **表格名稱** | **說明** |
|-----|-----|
| `Users` | 此 `users` 此表格包含註冊客戶的帳戶詳細資料，包括個人的電子郵件、名稱和註冊日期。 這可讓您分析不同的客戶區段及其購買行為。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 此 `orders` 表格可作為所有訂單層級量度的基礎。 這裡記錄的是從您購買的所有訂單詳細資料 [!DNL Spree] 商店，包括 `completed\_at` （訂單的時間戳記）， `user\_id` （下訂單的註冊使用者識別碼）。 如果訂單是由註冊使用者下達，則 `user\_id` 連結回到 `users` 此表格可分析使用者的購買行為。 |
| `Line items` | 此 `line\_items` 表格是以下任一專案的子項： `orders` 表格或 `subscriptions`. 它會記錄訂單或訂閱的行專案詳細資料。 針對具有多個產品的訂單，此表格中每個產品都有各自的資料列，包括 `product\_id` 可讓您將它連結至 `Products` 表格。 |
| `Products` | 此 `products` 表格會記錄您的Spree目錄中可銷售料號的所有產品明細。 這可讓您依產品屬性來劃分條列專案層級量度。 |
| `Subscriptions` | 如果您擁有 [!DNL Spree] 訂閱擴充功能， `subscriptions` 表格包含每個個別訂閱的資訊，包括 `created\_at` （開始日期）， `cancelled\_at` （取消訂閱的日期），以及 `interval` 訂閱的ID。 |

{style="table-layout:auto"}

## 相關：

* [正在連線 [!DNL Spree]](../integrations/spree.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
