---
title: 特殊筛选运算符
description: 了解创建报告或创建量度时在筛选器中使用的几个特殊运算符。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: 'https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%
---
# 筛选器选项

本主题探讨[创建报告](../../tutorials/using-visual-report-builder.md){: target="_blank"}或[创建量度](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}时`filters`中使用的几个特殊`operators`。

## `Filter Operators`

* `LIKE`模式匹配。 这必须结合使用通配符%（用于包含可变字母数的通配符）或_（用于通配符单个字母）。  例如，对于`Jake Stein`、`Jake Smith`或`Fake Smith`，限制`LIKE \_ake%`将返回true。  `Drake Smith`将返回false。

* `NOT LIKE`类似于上述模式匹配，但检查哪些模式不匹配。

* `IS`检查该列是`NULL`还是空的。

* `IS NOT`类似于上面的`IS`运算符，但检查非NULL列。

* `IN`检查以逗号分隔的列表中是否存在值。 （例如，“颜色`IN`红色，橙色”等同于颜色`equal to`红色或颜色`equal to`橙色）。

* `NOT IN`类似于上面的`IN`，但检查某个值的缺失。
