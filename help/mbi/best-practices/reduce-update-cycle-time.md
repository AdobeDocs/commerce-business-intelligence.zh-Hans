---
title: 缩短更新周期
description: 了解如何缩短更新周期时间。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# 缩短更新周期处理时间

[!DNL Adobe Commerce Intelligence]整天与您的数据库同步以复制新数据，确保您的仪表板始终显示最新信息。

许多因素都会增加本已冗长的更新时间。 某些复制方法、更高的重新检查频率以及功能板和图表的数量只是少数几个因素。 本主题将讨论缩短更新时间的一些最佳实践。

## 降低重新检查频率

在数据库表中，可以存在具有可变值的数据列。 例如，在&#x200B;**订单**&#x200B;表中可能有一个名为&#x200B;**状态**&#x200B;的列。 最初将订单写入数据库时，状态列可能包含值`pending`。 已在您的[Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)中使用此`pending`值复制该订单。

可更改列必须在一段时间内重新检查[更新的值](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)。 默认情况下，[!DNL Commerce Intelligence]在每次更新时都会重新检查这些列，但如果要重新检查和复制的数据量很大，则可能会对更新时间产生负面影响。 Adobe建议将重新检查频率设置为每日、每周或每月，而不是在每次更新时运行重新检查。

## 使用增量复制方法

如上所述，较长的更新时间与必须重新检查和复制的数据量直接相关。 [增量复制方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)可以大大减少在更新周期期间处理的数据量。 Adobe建议尽可能使用这些方法或修改数据库以支持增量方法。

## 从功能板中删除未使用的图表

在更新周期结束时，[!DNL Commerce Intelligence]对所有图表执行缓存操作。 高速缓存存储数据，以便将来能够更快地完成信息请求。 在[!DNL Commerce Intelligence]中，这意味着仪表板加载速度很快，因为图表不需要在每次加载时查询数据。

由于[!DNL Commerce Intelligence]只对仪表板中找到的图表执行缓存操作，因此从仪表板中删除未使用的图表会缩短更新时间。 请记住，同一图表可能位于多个功能板上 — 请与您的团队确认，确保他们也移除了任何未使用的图表。

>[!NOTE]
>
>从仪表板中删除图表不会删除图表。 您可以[随时将其添加回来](../data-user/dashboards/add-charts-dashboard.md)。

## 优化数据库以进行分析

除了重新评估重新检查频率、复制方法和图表有用性之外，您还可以[优化数据库以进行分析](../best-practices/opt-db-analysis.md)。

## 正在结束

如果在实施这些建议后，您的更新时间似乎仍然很慢，请[联系支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
