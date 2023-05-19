---
title: 新架構
description: 瞭解遷移至新架構的好處。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 新架構

[!DNL Adobe Commerce Intelligence] 過去一年，產品與工程團隊一直專注於儘可能進行最全面、最符合需求的改進。 Adobe很高興宣佈推出新功能 [!DNL Commerce Intelligence] 讓這些改善成為現實的產品架構。

## 新架構的優點

* 在Data Warehouse中建立欄型別，包括使用SQL的計算欄。
* 新欄可立即使用。
* 資料延遲大幅改善。

## 技術優點

主要差異列於上面，但主要變更是在更新週期期間執行計算的方式。 在每次更新期間，計算不再在每個欄上執行；而是從視覺Report Builder隨選執行。

### 遷移至新架構

由於帳戶的基本建設方式不同，因此不會自動將您的Data Warehouse或報表移轉至新的架構帳戶。 遷移至新架構需要重新實作您現有的帳戶。

### 遷移至新架構的成本

沒有新增成本！ Adobe會為您建立此新帳戶，以開始重新實作，至少有一個月的免費時間。 這可讓您有時間開啟兩個帳戶，以便更輕鬆地執行重新實作，並確保您的團隊沒有服務間隙。

### 在新架構中重新實作帳戶所需的時間

重新實作時間視您要重建的內容而異。 Adobe建議您在現有帳戶中執行下列步驟，以瞭解重新實作中會涉及哪些內容：

* 識別一組核心報表/控制面板。
* 識別建立這些報表所需的量度和維度。
* 識別重新建立這些量度和維度所需的欄。

完成此程式後，您就會知道哪些資料需要同步至新架構Data Warehouse，才能重新建置這些核心報表。

### 取得協助

此 [!DNL Adobe Commerce Intelligence] [服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 您只需額外付費即可執行重新實作。 聯絡您的 [Adobe客戶團隊](../../guide-overview.md#Submitting-a-Support-Ticket) 並準備好提供您想要優先在新帳戶中建立的儀表板/報告清單

### 繼續使用現有架構

如果這些功能對您來說並不重要，您可以繼續使用現有帳戶。 保留現有帳戶不需額外付費。 Adobe會持續支援這些帳戶，不會有任何變更。
