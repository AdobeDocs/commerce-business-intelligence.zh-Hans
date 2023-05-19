---
title: 選擇Report Builder
description: 瞭解如何選擇您的Report Builder。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# 選擇Report Builder

>[!NOTE]
>>需要 [管理員許可權](../../administrator/user-management/user-management.md).


現在您有了更多建立分析的選項，有時候可能很難確切知道哪一種風格的Report Builder適合您的需求。 本主題將引導您選擇最佳方法來建置分析。

## 何時應使用 [!DNL SQL Report Builder]？ {#whensql}

檢視您使用的一些常見原因 [!DNL SQL Report Builder] 超過 [!DNL traditional Report Builder].

### 如果您想使用 [!DNL SQL] — 特定函式……

美的一部分 [!DNL SQL Report Builder] 這讓您能夠使用Data Warehouse管理員中目前未提供的功能。 過去，分析師可能必須介入協助您完全實現您的願景。

此 [!DNL SQL Report Builder] 支援函式，例如 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 和 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)，而您先前無法使用。 您可以存取 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但其他一些SQL特定函式包括：

* [`Bitwise aggregate` 函式](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 運運算元](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果您想要執行一些測試……

如果您想嘗試不同的技巧和策略來找出最適合您的分析的技巧，您可能會想要使用 [!DNL SQL Report Builder]. 在「Data Warehouse管理員」中建置欄需要時間，而您使用DWM建立的欄則取決於更新週期。

您最多只能等待一個更新週期，然後才能使用欄。 如果您發現建立欄時發生錯誤，您必須等待 *二* 循環：一個用於初始填入欄，另一個用於傳播修訂版本的循環。

### 如果您只使用新欄一次……

如上節所述，在Data Warehouse管理員中建立欄需要時間。 如果您只打算使用一個您在報表中建立的欄，Adobe建議使用 [!DNL SQL Report Builder]. 如此一來，您就不必等待更新週期完成，而能更迅速地恢復工作。

### 如果您使用的資料具有一對多關係……

有時，資料的結構可能導致 [!DNL SQL Report Builder] 更有效率、更符合邏輯的選擇來建置您的分析。 在「Data Warehouse管理員」中直接建立一對一關係的欄，但當您處理一對多關係時，事情可能會有點混亂。

假設單一產品被視為多個產品類別的一部分，而您想要檢視與每個產品的每個類別相關聯的收入。 嘗試使用DWM建立這種關係可能既繁瑣又困難，但撰寫時 [!DNL SQL] 查詢可能更直接一些：

![](../../assets/When_should_I_use_the_RB_2.png)

## 我何時應使用傳統Report Builder？ {#whentraditionalrb}

而 [!DNL SQL Report Builder] 可讓您對先前無法使用的功能擁有更多控制權和存取權，但可能並不總是正確的選擇。 Adobe建議，在決定要使用哪種Report Builder風格時，也應考量下列事項。

### 如果您要建置簡單報表……

如果您要建立的內容簡單明瞭，則使用傳統Report Builder可能比撰寫完整檔案快得多 [!DNL SQL] 查詢。 如果您需要建立分析的任何欄已經在Data Warehouse管理員中，則此功能會很有幫助。

### 如果您正在與其他使用者共用您的工作……

貴組織的使用者是否使用/檢視此分析？ 視您與誰共用您的工作而定，有時候選擇視覺Report Builder可能更好。 使用者可快速檢視 [!DNL Visual Report Builder] 與讀取可能較長的專案 [!DNL SQL] 查詢。

如果有人需要報告但不熟悉 [!DNL SQL]，Adobe建議使用Report Builder的原始風格。 讓操作更輕鬆。

## 正在結束 {#wrapup}

兩者皆有 [!DNL SQL Report Builder] 和 [!DNL Visual Report Builder] 適用於多種使用案例。 這通常取決於您的分析需求以及誰在使用分析。
