---
title: SQL和Data Warehouse管理員之間的差異
description: 瞭解SQL和Data Warehouse管理員之間的差異。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 兩者之間的差異 [!DNL SQL] 和 [!DNL Data Warehouse Manager]

在中建立的欄之間有兩個主要差異 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 以及使用 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 一個是與更新週期的相依性，另一個是欄如何儲存在您的帳戶中。

## 中的欄 [!DNL SQL Report Builder]

欄不依賴於更新週期，因此您不再需要等待一個欄完成之後才能對欄進行迭代。 如果發生錯誤，只需按幾下按鍵即可進行修正，不必再等待兩次更新完成後再返回工作。

>[!IMPORTANT]
>
>您使用建立的欄 [!DNL SQL] 編輯器不會儲存至您的Data Warehouse。 您一律可以存取包含欄的查詢，但如果您想要在多個報表中使用欄，則必須在每個報表的查詢中重新建立該欄。 這表示欄是使用 [!DNL SQL] 編輯器無法用於傳統中 [!DNL Report Builder].

## Data Warehouse管理員中的欄

欄取決於更新週期，因此必須先完成一個完整的週期，然後才能進行編輯。 這些欄會儲存至Data Warehouse管理員，並可在傳統檔案中使用 [!DNL Report Builder] 或 [!DNL SQL Report Builder].
