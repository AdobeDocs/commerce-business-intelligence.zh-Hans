---
title: 修改数据库以支持增量复制
description: 了解如何修改数据库以支持增量复制。
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 334
ht-degree: 0%

---

# 支持增量复制

如果您的表当前不允许增量复制，请参阅以下建议以了解可能的解决方案。

## 修改时间

`Modified At`方法是最理想的复制方法，它使用`datetime`列检测新的和/或更新数据。 请记住，使用此方法的表中的列`datetime`必须编制索引，且不能随时包含null值。

如果您的表没有`datetime`列，则可以添加索引`modified at`列。 `modified at`列中不允许有Null值。 检查是否为每行填充该列。

为确保`Modified At`方法按预期工作，您无法从表中删除行。 您应该通过向表中添加`deleted`列来将该行标记为无效。 如果行无效，此列返回`1`，否则返回`0`。 然后，在构建量度和报表时，您可以使用此列过滤掉无效行。

## 对单个自动递增主键的修改

如果无法启用`Modified At`方法，则“单个自动递增主键”是下一个最佳选项。 通过搜索高于Data Warehouse中当前最高值的主键值，使用此方法可在表中发现新数据。

请记住，使用此方法的表是带整数自动递增主键的单列。 要在数据库中使用此方法，请进行以下修改：

* 如果主键是复合键或非整数，请将主键更改为自动递增整数
* 如果主键是单整数列，但键可以按非顺序分配，则将主键更改为自动递增

## 正在结束

通过对表进行细微的修改，您可以利用更快、更有效的增量复制方法。 但是，如果无法执行此操作，您仍可采取其他步骤[缩短更新时间](../best-practices/reduce-update-cycle-time.md)和[优化数据库](../best-practices/opt-db-analysis.md)。
