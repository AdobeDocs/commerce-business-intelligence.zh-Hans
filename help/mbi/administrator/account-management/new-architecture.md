---
title: 新架构
description: 了解迁移至新架构的好处。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# 新架构

[!DNL Adobe Commerce Intelligence]产品和工程团队在过去一年中一直专注于尽可能进行最广泛、请求量最大的改进。 Adobe很高兴地宣布推出新的[!DNL Commerce Intelligence]产品架构，以实现这些改进。

## 新架构的优势

* 在Data Warehouse中创建类型的列，包括使用SQL的计算列。
* 新列将立即可用。
* 数据延迟显着改善。

## 技术优势

上面列出了主要差异，但主要更改是在更新周期中执行计算的方式。 在每次更新期间，计算不再在每列上运行；而是从Visual Report Builder中按需运行。

### 迁移到新架构

由于帐户的基本构建方式不同，因此不会自动将您的Data Warehouse或报表迁移到新的架构帐户。 要迁移至新架构，需要重新实施您的现有帐户。

### 迁移至新架构的成本

无额外成本！ Adobe将为您创建此新帐户以开始重新实施，至少一个月免费。 这样，您就有时间打开这两个帐户，以便更轻松地执行重新实施，并确保您的团队在服务上不存在缺口。

### 在新架构中重新实施帐户所需的时间

重新实施时间因您要重建的内容而异。 Adobe建议您在现有帐户中执行以下步骤，以了解重新实施中将涉及的内容：

* 确定一组核心报表/功能板。
* 确定构建这些报表所需的指标和维度。
* 确定重新创建这些量度和维度所需的列。

完成后，您将知道哪些数据需要同步到新架构Data Warehouse以重建这些核心报告。

### 获取帮助

[!DNL Adobe Commerce Intelligence] [服务团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)可以执行重新实施，但需支付额外费用。 请联系您的[Adobe客户团队](../../guide-overview.md#Submitting-a-Support-Ticket)，并准备好提供您希望在新帐户中优先创建的功能板/报告列表

### 保持现有体系结构

如果这些功能对您来说并不重要，您可以继续使用现有帐户。 保留现有帐户无需额外付费。 Adobe将继续支持这些帐户，并且不会做任何更改。
