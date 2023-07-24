---
title: 新架构
description: 了解迁移到新架构的好处。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 新架构

[!DNL Adobe Commerce Intelligence] 过去一年，产品和工程团队一直专注于尽可能进行最全面、最符合要求的改进。 Adobe很高兴宣布推出一款新产品 [!DNL Commerce Intelligence] 使这些改进成为现实的产品体系结构。

## 新架构的好处

* 在Data warehouse中创建列类型，包括带SQL的计算列。
* 新列将立即可用。
* 数据延迟显着改善。

## 技术优势

上面列出了主要差异，但主要更改是在更新周期中执行计算的方式。 在每次更新期间，不再在每列上运行计算；而是按需从可视化Report Builder中运行计算。

### 迁移到新架构

由于客户的基本结构不同，因此不会自动将您的Data warehouse或报告迁移到新的架构客户。 迁移到新架构需要重新实施您的现有帐户。

### 迁移至新架构的成本

没有增加成本！ Adobe将为您创建此新帐户以开始重新实施，至少在一个月内免费。 这样，您就有时间打开这两个帐户，以便更轻松地执行重新实施，并确保您的团队不存在服务缺口。

### 在新架构中重新实施帐户所需的时间

重新实施时间因您要重建的内容而异。 Adobe建议您在现有帐户中执行以下步骤，以了解重新实施所涉及的步骤：

* 确定一组核心报表/功能板。
* 确定构建这些报表所需的量度和维度。
* 确定重新创建这些量度和维度所需的列。

完成后，您会知道需要同步到新架构Data warehouse的数据，以便重建这些核心报告。

### 获取帮助

此 [!DNL Adobe Commerce Intelligence] [服务团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 可以执行重新实施，但需支付额外费用。 联系 [Adobe客户团队](../../guide-overview.md#Submitting-a-Support-Ticket) 并准备好提供您希望在新帐户中优先创建的功能板/报表的列表

### 继续使用现有架构

如果这些功能对您来说并不重要，您可以继续使用现有帐户。 保留现有帐户无需额外付费。 Adobe将继续支持这些帐户，而不会做任何更改。
