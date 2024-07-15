---
title: 数据和更新信息
description: 了解如何检查更新周期的状态。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 数据和更新信息

* [为什么我的数据发生了更改？](#datachange)
* [定期更新和强制更新之间有何区别？](#regularforcedupdates)
* [为什么更新周期需要很长时间？](#updatecycletime)
* [更新周期完成时是否可以通知我？](#notifyupdate)
* [为什么 [!DNL Google ECommerce] 数据与我的数据库不同？](#ecommdatabase)
* [如何解决数据不一致问题？](#datadiscrepancy)

## 为什么我的数据发生了更改？ {#datachange}

由于新数据正在同步到您的Data Warehouse，图表值在一天中可能会发生更改。 此外，由于[重新检查](../data-warehouse-mgr/cfg-data-rechecks.md)，现有数据列的值可能会更改。 重新检查是一个在数据列中查找已更改值的进程，例如从`open`移至`shipped`的订单状态。

有几种不同的方式[可以检查更新周期](../../best-practices/check-update-cycle.md)的状态，具体取决于用户的权限设置。

## 定期更新和强制更新之间有何区别？ {#regularforcedupdates}

定期更新是&#x200B;**已计划的**&#x200B;进程，而强制更新是由您启动的&#x200B;**手动进程**。 如果您有封锁时间（或[!DNL Commerce Intelligence]不应更新您的数据的时间段），则强制更新会启动一个不遵守封锁期限制的周期。

## 为什么更新周期需要很长时间？ {#updatecycletime}

许多因素都会增加本已冗长的更新时间。 某些[复制方法](../data-warehouse-mgr/cfg-replication-methods.md)、[更高的重新检查频率](../data-warehouse-mgr/cfg-data-rechecks.md)以及仪表板和图表的数量只是少数参与者。 Adobe建议[重新配置某些设置](../../best-practices/reduce-update-cycle-time.md)和[优化数据库以进行分析](../../best-practices/opt-db-analysis.md)以减少更新时间。

## 更新周期完成时是否可以通知我？ {#notifyupdate}

如果更新正在进行，则`Connections`页面上有一个链接，您可以在周期完成后使用该链接请求电子邮件通知。

## 为什么[!DNL Google ECommerce]数据与我的数据库不同？ {#ecommdatabase}

[!DNL Google Analytics]和数据库之间的差异可能由各种原因引起。 跟踪未正确启用、用户访问无痕以及点击事件未正确工作只是几个示例。 如果您的收入和订单看起来不正确，[请查看此主题](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html)以诊断问题。

## 如何解决数据不一致问题？ {#datadiscrepancy}

Adobe知道，看到不一致的数据可能会让人感到沮丧。 尝试使用[数据差异核对清单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html)或[数据导出教程](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html)来诊断问题。 如果您仍然被阻塞，[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
