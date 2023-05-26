---
title: 特殊筛选运算符
description: 了解创建报告或创建量度时在筛选器中使用的几个特殊运算符。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 筛选器选项

本主题探讨了一些 `operators` 使用位置 `filters` 时间 [创建报告](../../tutorials/using-visual-report-builder.md){： target=&quot;_blank&quot;}或 [创建量度](../../data-user/reports/ess-manage-data-metrics.md){： target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` 模式匹配。 此参数必须结合使用通配符%（用于包含可变字母数的通配符）或_（用于通配符单个字母）。  例如，限制 `LIKE \_ake%` 将返回true `Jake Stein`， `Jake Smith`，或 `Fake Smith`.  将返回false `Drake Smith`.

* `NOT LIKE` 类似于上面的模式匹配，但检查哪些模式不匹配。

* `IS` 检查列是否为 `NULL`，或为空。

* `IS NOT` 类似于 `IS` 运算符，但检查非NULL列。

* `IN` 检查以逗号分隔的列表中是否存在值。 (例如，“颜色” `IN` “红色，橙色”等同于颜色 `equal to` 红色或颜色 `equal to` 橙色)。

* `NOT IN` 类似于 `IN` 以上，但检查某个值的缺失。
