---
title: 首次购买报告的平均时间
description: 了解如何使用平均首次购买时间报表。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 0%

---

# 首次购买报告的平均时间

许多Adobe客户都有一个名为`Average time to first purchase`的量度和图表，该量度和图表显示了一组用户注册日期与首次购买日期之间的平均时间。 随着时间越来越接近现在，数据几乎总是会向下倾斜。

![平均第一笔订购时间](../../assets/average-time-to-first-order.png)

这是因为这些较新的客户还没有机会生成从加入日期起超过一个月的任何购买。 由于从未购买过产品的用户根本不会包括在内（直到他们真的购买产品），因此这会使较新客户群的平均购买量出现下调。

还有其他几种可能的方法来看待这个指标，它们引入的偏见较少。 浏览一个示例。

## 示例：对第一笔订单执行`cohort`分析

您的`Users`仪表板中可能有一个名为`Time to first order cohort`的图表。 此报表使用`Distinct buyers`量度，按`cohort`周或注册月对用户进行分组，并显示在注册后接下来的几周或几个月内首次购买的用户比例（介于`0`和`1`之间）。

图表可能会显示，对于在2014年12月注册的用户，`0.56`（或`56%`）在第2个月（例如，2015年1月）之前做了第一笔订单。

此同类群组分析可很好地指示一段时间内用户激活率。 如果此图表开始扁平化或停滞不前，并且您仍未接近完全转化为购买者，则可能是时候通过电子邮件促销活动激活其余用户了。
