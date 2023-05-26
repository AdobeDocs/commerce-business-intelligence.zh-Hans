---
title: 缩短更新周期
description: 了解如何缩短更新周期时间。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 缩短更新周期处理时间

[!DNL Adobe Commerce Intelligence] 全天与数据库同步以复制新数据，确保仪表板始终显示最新信息。

许多因素都会增加原本就漫长的更新时间。 某些复制方法、更高的重新检查频率以及仪表板和图表数量只是少数几个因素。 本主题将讨论缩短更新时间的一些最佳实践。

## 降低重新检查频率

在数据库表中，可以存在具有可变值的数据列。 例如，在 **订单** 表可能有一个名为的列 **状态**. 最初将订单写入数据库时， status列可能包含值 `pending`. 订单会复制到您的 [data warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) 使用此 `pending` 值。

可更改列必须为 [已重新检查更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 随着时间推移。 默认情况下， [!DNL Commerce Intelligence] 在每次更新期间都会重新检查这些列，但如果要重新检查和复制的数据量很大，则可能会对更新时间产生负面影响。 Adobe建议将重新检查频率设置为每日、每周或每月，而不是在每次更新期间运行重新检查。

## 使用增量复制方法

如上所述，较长的更新时间与必须重新检查和复制的数据量直接相关。 [增量复制方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 可以显着减少更新周期期间处理的数据量。 在可能的情况下，Adobe建议使用这些方法或修改数据库以支持增量方法。

## 从功能板中删除未使用的图表

在更新周期结束时， [!DNL Commerce Intelligence] 对所有图表执行缓存操作。 缓存存储数据，以便将来能够更快地完成信息请求。 In [!DNL Commerce Intelligence]，这意味着仪表板加载迅速，因为图表不需要在每次加载时查询数据。

从 [!DNL Commerce Intelligence] 仅对功能板中找到的图表执行缓存操作，从功能板中删除未使用的图表会缩短更新时间。 请记住，同一图表可能位于多个功能板上 — 请与您的团队联系，确保他们也移除了任何未使用的图表。

>[!NOTE]
>
>从功能板中删除图表不会删除图表。 您可以 [可随时重新添加](../data-user/dashboards/add-charts-dashboard.md).

## 优化数据库以进行分析

除了重新评估重新检查频率、复制方法和图表有用性之外，您还可以 [优化数据库以进行分析](../best-practices/opt-db-analysis.md).

## 总结

如果实施这些建议后，您的更新时间似乎仍较慢， [联系支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
