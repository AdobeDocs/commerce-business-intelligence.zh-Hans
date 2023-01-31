---
title: 特殊过滤器运算符
description: 了解在创建报表或创建量度时过滤器中使用的一些特殊运算符。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 筛选选项

在本文中，我们将探索一些特殊的 `operators` 在 `filters` when [创建报告](../../tutorials/using-visual-report-builder.md){:target=&quot;_blank&quot;}或 [创建量度](../../data-user/reports/ess-manage-data-metrics.md){:target=&quot;_blank&quot;}。

## `Filter Operators`

* `LIKE` 模式匹配。 这必须与通配符%（对于具有可变字母数的通配符）或_（对于通配符单字母）一起使用。  例如，限制 `LIKE \_ake%` 将返回true `Jake Stein`, `Jake Smith`或 `Fake Smith`.  对于，它将返回false `Drake Smith`.

* `NOT LIKE` 与上面的模式匹配类似，但会检查哪些模式不匹配。

* `IS` 检查列是否为 `NULL`，或为空。

* `IS NOT` 与 `IS` 运算符，但检查非NULL列。

* `IN` 检查值在以逗号分隔的列表中是否存在。 (例如，“颜色” `IN` red，orange”等同于颜色 `equal to` 红色或颜色 `equal to` 橙色)。

* `NOT IN` 类似于 `IN` ，但会检查值是否缺失。
