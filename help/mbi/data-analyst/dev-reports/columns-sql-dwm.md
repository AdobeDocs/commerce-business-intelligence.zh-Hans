---
title: SQL和Data Warehouse管理器之间的区别
description: 了解SQL和Data Warehouse管理器之间的区别。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 之间的差异 [!DNL SQL] 和 [!DNL Data Warehouse Manager]

在中创建的列之间存在两个关键差异 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 以及使用 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 一个是与更新周期的依赖关系，另一个是列在帐户中的保存方式。

## 中的列 [!DNL SQL Report Builder]

列不依赖于更新周期，因此无需再等待一个列完成即可对列进行迭代。 如果犯错，只需按几下键即可更正，不必再等待两次更新完成后才能重新开始工作。

>[!IMPORTANT]
>
>您使用 [!DNL SQL] 编辑器未保存到Data Warehouse中。 您始终可以访问包含列的查询，但如果您要在多个报表中使用列，则必须在每个报表的查询中重新创建该列。 这意味着使用创建的列 [!DNL SQL] 不能在传统中使用编辑器 [!DNL Report Builder].

## Data Warehouse管理器中的列

列取决于更新周期，因此必须先完成一个完整的周期，然后才能对其进行编辑。 这些列将保存到Data Warehouse管理器中，并可在传统模板中使用 [!DNL Report Builder] 或 [!DNL SQL Report Builder].
