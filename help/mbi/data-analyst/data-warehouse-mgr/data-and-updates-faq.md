---
title: 数据和更新信息
description: 了解如何检查更新周期的状态。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 数据和更新信息

* [为什么我的数据发生了更改？](#datachange)
* [定期更新和强制更新之间有何区别？](#regularforcedupdates)
* [为什么更新周期需要很长时间？](#updatecycletime)
* [更新周期完成时是否可以通知我？](#notifyupdate)
* [为什么是 [!DNL Google ECommerce] 与我的数据库不同的数据？](#ecommdatabase)
* [如何解决数据不一致问题？](#datadiscrepancy)

## 为什么我的数据发生了更改？ {#datachange}

由于新数据正在同步到您的Data Warehouse，图表值在一天中可能会发生更改。 此外，现有数据列的值可能由于以下原因而更改 [重新检查](../data-warehouse-mgr/cfg-data-rechecks.md). 重新检查是一个在数据列中查找已更改值的进程，例如从移出的订单状态 `open` 到 `shipped`.

有几种不同的方式 [检查更新周期的状态](../../best-practices/check-update-cycle.md)，具体取决于用户的权限设置。

## 定期更新和强制更新之间有何区别？ {#regularforcedupdates}

定期更新包括 **已计划** 强制更新时执行的进程 **由您启动的手动流程**. 如果您有中断小时数(或 [!DNL Commerce Intelligence] 不应更新您的数据)，强制更新会启动一个不遵守封锁期限制的周期。

## 为什么更新周期需要很长时间？ {#updatecycletime}

许多因素都会增加本已冗长的更新时间。 特定 [复制方法](../data-warehouse-mgr/cfg-replication-methods.md)， [较高的复检频率](../data-warehouse-mgr/cfg-data-rechecks.md)、功能板和图表的数量仅为少数参与者。 Adobe推荐 [重新配置某些设置](../../best-practices/reduce-update-cycle-time.md) 和 [优化数据库以进行分析](../../best-practices/opt-db-analysis.md) 以减少更新时间。

## 更新周期完成时是否可以通知我？ {#notifyupdate}

如果更新正在进行，则在 `Connections` 周期完成后可用于请求电子邮件通知的页面。

## 为什么是[!DNL Google ECommerce]与我的数据库不同的数据？ {#ecommdatabase}

之间的差异 [!DNL Google Analytics] 并且数据库可能由于各种原因而产生。 跟踪未正确启用、用户访问无痕以及点击事件未正确工作只是几个示例。 如果你的收入和订单不合理， [请参阅此主题](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 以诊断问题。

## 如何解决数据不一致问题？ {#datadiscrepancy}

Adobe知道，看到不一致的数据可能会让人感到沮丧。 尝试使用 [数据差异核对清单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) 或 [数据导出教程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) 以诊断问题。 如果你还受累的话， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
