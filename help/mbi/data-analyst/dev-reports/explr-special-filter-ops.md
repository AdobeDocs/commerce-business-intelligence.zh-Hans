---
title: 特殊筛选运算符
description: 了解创建报告或创建量度时在筛选器中使用的几个特殊运算符。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 筛选器选项

本主题探讨`operators`创建报告`filters`或[创建量度](../../tutorials/using-visual-report-builder.md){: target="_blank"}时[中使用的几个特殊](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}。

## `Filter Operators`

* `LIKE`模式匹配。 这必须结合使用通配符%（用于包含可变字母数的通配符）或_（用于通配符单个字母）。  例如，对于`LIKE \_ake%`、`Jake Stein`或`Jake Smith`，限制`Fake Smith`将返回true。  `Drake Smith`将返回false。

* `NOT LIKE`类似于上述模式匹配，但检查哪些模式不匹配。

* `IS`检查该列是`NULL`还是空的。

* `IS NOT`类似于上面的`IS`运算符，但检查非NULL列。

* `IN`检查以逗号分隔的列表中是否存在值。 （例如，“颜色`IN`红色，橙色”等同于颜色`equal to`红色或颜色`equal to`橙色）。

* `NOT IN`类似于上面的`IN`，但检查某个值的缺失。
