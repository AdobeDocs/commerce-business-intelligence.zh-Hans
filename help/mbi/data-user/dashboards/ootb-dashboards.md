---
title: 包含的仪表板
description: 了解如何检查关键量度的运行状况，例如用户生命周期收入、重复购买次数等，从而为未来探索奠定坚实的基础。
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# 包含的仪表板

[!DNL Adobe]提供`eCommerce`和`SaaS`入门程序包。 这些由Adobe分析师创建的包包含适用于您的数据集的自定义功能板和报表集。 通过这些资源包中包含的分析，可检查关键量度的运行状况，如用户生命周期收入、重复购买次数等，从而为未来的探索奠定坚实的基础。

>[!NOTE]
>
>某些功能板的可用性取决于您的数据集。

如果您有疑问或有兴趣向帐户添加程序包，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以获取帮助。

## 执行概述

`executive overview`仪表板是从其他仪表板上的图表生成的。 该仪表板是数据的高级概述，包含每天都会查看的图表，而其他仪表板则包含更详细的信息。 最初，它被设置为每个帐户中的默认仪表板。

其中包含了一组常规图表。 Adobe建议通过添加您最常使用的其他图表，根据您的需求定制此仪表板。

## 同类群组分析

`cohort analysis`仪表板包括一组图表，这些图表显示按注册同类群组分组的平均用户生命周期收入增长和增量收入增长。 此项可揭示客户存留期价值(LTV)、客户对企业的价值是否随时间的推移而增加，还可识别有关LTV增长的趋势。 默认情况下，在平均LTV计算中，*所有注册用户（购买者和非购买者）都被考虑在内* — 请参阅[同类群组分析主题](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。

此仪表板可能还包括用于分析特定客户获取来源、渠道或人口统计（例如，纽约或加利福尼亚）的用户生命周期收入的同类群组图表。 这是为了演示如何分析用户群中特定区段的LTV，并查看一个组或另一个组是否随时间推移产生更高的LTV。

有关同类群组的详细信息，请参阅[执行同类群组分析](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。

如果您当前未跟踪用户获取来源，请参阅[跟踪用户获取Source数据概述](../../data-analyst/analysis/google-track-user-acq.md)。

## 电子邮件摘要

`Email Summary`仪表板包含一组可在每日自动电子邮件摘要中使用的示例图表。 有关配置电子邮件摘要的详细信息，请参阅[创建自动电子邮件摘要](../../data-user/export-data/email-summaries.md)。  

## 维系状况

`Retention health`仪表板显示您的用户群的重复购买行为。

`Time between orders`图表显示用户在第一和第二顺序、第二和第三顺序等之间经过的平均时间和/或中间值。 您可以[考虑使用此数据来配置您的电子邮件营销活动](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)。

`Users by lifetime number of orders`图表列出每个生命周期订单数中的用户总数，以提供重复购买行为的概述。  

`Repeat order probability`图表显示具有特定订单号的用户重复购买的可能性。 要查看客户下了`x`次订单以发出`(x+1)`次订单的概率，只需将购买次数至少为`(x+1)`的人数除以购买次数至少为`x`的人数即可。

### 示例

在其存留期内购买过一次的客户数： `90`

在其存留期内购买两次的客户数： `30`

在其一生中购买过三次的客户数： `10`

在此示例中，在其有生之年购买一次以第二次购买的客户的重复订购概率为： `(30 + 10) / (30+10+90) = 30.77%`。

## 客户LTV增长

`Customer LTV growth`仪表板包含一组图表，用于查找每个用户的平均收入。 这些图表基于注册后头30、60、90或365天内产生的平均收入进行分段。  

图表的下方行显示按客户获取来源或人口统计划分的这些平均值，以显示随着时间推移哪些用户组产生的收入最多。

## 产品性能

`Product Performance`仪表板包括一些图表，这些图表通过按项显示销售项数和收入并识别表现最好的产品来显示一般产品表现。

## 最近活动

`Recent Activity`仪表板显示过去30天的性能数据。

## 事务运行状况

`Transaction Health`仪表板包括收入、订单和平均订单值的概览图表。 这些图表可以按营销渠道、人口统计或特殊优惠券代码进行分段。

## 要定位的用户

`Users to target`仪表板包括表格样式图表，这些图表列出了具有共同特定购买行为的用户。 一些示例包括：

* `X`个月前购买过的一次性购买者列表（您可能希望重新激活的对象）

* 顶级消费者（您可能希望让谁开心）列表

* 过去`X`天内活跃的顶级支出者列表（您可能希望奖励哪些人）

使用您的数据导出工具，可以轻松[创建目标营销中具有类似购买行为的用户的电子邮件列表](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/)。

## 用户活动

`User activity`仪表板包括按各种数据（包括客户获取来源、人口统计和平均首次订购）划分用户的图表。 其中还包括用户同类群组分析，包括按用户注册月份划分的总平均生命周期收入。

`% of cohort members who have purchased`图表很有价值，因为它显示基于用户注册时间的转化率（从0到1）（每行表示用户同类群组）。 它还显示客户首次购买的时间（例如，注册后1、2、3...月）。 该报表可能会显示10%的用户在第1个月激活，而此数字在第2、3、4个月增长……并可能在以后停止增长。

通常，在一段时间后，此图表中的线条会变为水平线。 这表明，在该时间点之后，几乎没有其他同类群组成员会进行有机转化 — 大多数即将购买的用户已经完成了转化。 目前，这些成员国极不可能在没有干预的情况下转化为购买者。 [通过自定义促销活动或定向电子邮件联系他们是一种快速启动此群体转换的低风险方法。](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
