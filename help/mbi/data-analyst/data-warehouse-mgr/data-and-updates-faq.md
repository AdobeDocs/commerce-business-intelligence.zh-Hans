---
title: 数据和更新信息
description: 了解如何检查更新周期的状态。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 数据和更新信息

* [为什么我的数据会发生更改？](#datachange)
* [定期更新和强制更新之间有何区别？](#regularforcedupdates)
* [更新周期为何需要很长时间？](#updatecycletime)
* [更新周期完成后，是否可以通知我？](#notifyupdate)
* [为什么 [!DNL Google ECommerce] 数据与我的数据库不同？](#ecommdatabase)
* [如何排查数据差异？](#datadiscrepancy)

## 为什么我的数据会发生更改？ {#datachange}

由于新数据会同步到您的data warehouse，因此图表值会在一天中发生更改。 此外，现有数据列的值可能会因 [重新检查](../data-warehouse-mgr/cfg-data-rechecks.md). 重新检查是一个过程，它会在数据列中查找更改的值，例如，顺序状态从 `open` to `shipped`.

有几种不同的方式 [检查更新周期的状态](../../best-practices/check-update-cycle.md)，具体取决于您拥有的用户权限类型。

## 定期更新和强制更新之间有何区别？ {#regularforcedupdates}

定期更新包括 **计划** 强制更新时的进程 **由您启动的手动流程**. 如果您有封锁时间，或 [!DNL MBI] 不应更新您的数据 — 强制更新将启动一个不遵守封锁期限制的周期。

## 更新周期为何需要很长时间？ {#updatecycletime}

大量因素可能会增加本已非常漫长的更新时间。 特定 [复制方法](../data-warehouse-mgr/cfg-replication-methods.md), [更高的重检频率](../data-warehouse-mgr/cfg-data-rechecks.md)，而功能板和图表的数量只是少数参与者。 我们建议 [重新配置某些设置](../../best-practices/reduce-update-cycle-time.md) 和 [优化数据库以进行分析](../../best-practices/opt-db-analysis.md) 以缩短更新时间。

## 更新周期完成后，是否可以通知我？ {#notifyupdate}

当然！ 如果当前正在进行更新，则 `Connections` 页面，在周期结束后，您可以使用该页面请求电子邮件通知。

## 为什么[!DNL Google ECommerce]数据与我的数据库不同？ {#ecommdatabase}

之间的差异 [!DNL Google Analytics] 数据库的出现有多种原因。 未正确启用跟踪、隐身访问用户以及点击事件无法正常工作只是少数示例。 如果你的收入和订单看起来不太对， [使用本文](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) 来诊断问题。

## 如何排查数据差异？ {#datadiscrepancy}

我们知道，看到不一致的数据可能是令人沮丧的体验。 尝试使用我们的 [数据差异核对清单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) 或 [数据导出教程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) 来诊断问题。 如果你仍然被难住， [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
