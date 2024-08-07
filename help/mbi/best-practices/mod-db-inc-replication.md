---
title: 修改数据库以支持增量复制
description: 了解如何修改数据库以支持增量复制。
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
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
