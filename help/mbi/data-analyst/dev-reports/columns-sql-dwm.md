---
title: SQL和Data Warehouse Manager之间的区别
description: 了解SQL和Data Warehouse Manager之间的差异。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# [!DNL SQL]和[!DNL Data Warehouse Manager]之间的差异

在[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)中创建的列与使用[[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md)创建的列之间存在两个关键差异。 一个是与更新周期的依赖关系，另一个是列在帐户中的保存方式。

## [!DNL SQL Report Builder]中的列

列不依赖于更新周期，因此无需再等待一个列完成即可对列进行迭代。 如果犯错，只需按几下键即可更正，不必再等待两次更新完成后才能重新开始工作。

>[!IMPORTANT]
>
>使用[!DNL SQL]编辑器创建的列未保存到Data Warehouse。 您始终可以访问包含列的查询，但如果您要在多个报表中使用列，则必须在每个报表的查询中重新创建该列。 这意味着使用[!DNL SQL]编辑器创建的列不能在传统[!DNL Report Builder]中使用。

## Data Warehouse Manager中的列

列取决于更新周期，因此必须先完成一个完整的周期，然后才能对其进行编辑。 这些列将保存到Data Warehouse管理器，并可在传统[!DNL Report Builder]或[!DNL SQL Report Builder]中使用。
