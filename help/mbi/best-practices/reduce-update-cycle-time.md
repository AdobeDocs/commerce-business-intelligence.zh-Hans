---
title: 缩短更新周期
description: 了解如何缩短更新周期。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# 缩短更新周期处理时间

[!DNL MBI] 一天之内与数据库同步以复制新数据，从而确保功能板始终显示最新信息。

大量因素可能会增加本已非常漫长的更新时间。 某些复制方法、更高的重新检查频率以及功能板和图表的数量只是少数贡献因素。 本主题讨论了一些减少更新时间的最佳实践。

## 减少重新检查频率

在数据库表中，可以有具有可更改值的数据列。 例如，在 **订购** 表中可能有一个名为 **状态**. 当订单最初写入数据库时，状态列可能包含值 `pending`. 随后，订单将复制到 [data warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) 此 `pending` 值。

可更改的列需要为 [重新检查更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 随着时间推移。 默认情况下， [!DNL MBI] 在每次更新期间都会重新检查这些列，但如果要重新检查和复制大量数据，可能会对更新时间造成负面影响。 我们建议将重新检查频率设置为每日、每周或每月，而不是在每次更新期间运行重新检查。

## 使用增量复制方法

如上所述，较长的更新时间会直接与需要重新检查和复制的数据量相关。 [增量复制方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) 可以大大减少更新周期中处理的数据量。 我们建议尽可能使用这些方法或对数据库进行修改以支持增量方法。

## 从功能板中删除未使用的图表

在更新周期结束时， [!DNL MBI] 对所有图表执行缓存操作。 缓存会存储数据，以便能够更快地完成未来的信息请求。 在 [!DNL MBI]，这意味着功能板将快速加载，因为图表在每次加载时都不需要查询数据。

自 [!DNL MBI] 仅对功能板中找到的图表执行缓存操作，从功能板中删除未使用的图表将减少更新时间。 请记住，同一图表可能位于多个功能板上 — 请咨询您的团队，确保它们也删除了任何未使用的图表。

>[!NOTE]
>
>从功能板中删除图表不会删除图表。 您可以 [随时将其添加回](../data-user/dashboards/add-charts-dashboard.md).

## 优化数据库以进行分析

除了重新评估重新检查频率、复制方法和图表的有用性之外，您还可以 [优化数据库以进行分析](../best-practices/opt-db-analysis.md).

## 包装

如果即使在实施这些建议后更新时间仍显缓慢， [联系我们的支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
