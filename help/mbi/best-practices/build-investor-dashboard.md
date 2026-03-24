---
title: 为投资者构建功能板
description: 了解如何为投资者构建仪表板。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Developer, User
feature: Dashboards, Data Integration
TQID: https://experienceleague.adobe.com/0G3u84SK-CvA7Pvb5bI-uEkUkbi9oiYvWwJHRwd-568
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 289
ht-degree: 0%

---

# 构建投资者信息板

许多客户与投资者合作，因此需要从该平台共享信息，但您为制定日常业务决策而创建的功能板可能不是投资者所寻求的。 下面介绍了一些最佳实践，介绍如何创建全面但简单的功能板，非常适合与活跃和潜在投资者共享。

以下是您需要为投资人信息板创建报告的内容：

## 标量报表

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## 可视化报表

* **[!UICONTROL Revenue by quarter]**
   * 量度 — 收入
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 量度 — 首次订单收入
      * 过滤器 — 用户的订单号等于1
   * 量度2 — 重复订单收入
      * 筛选器 — 用户的订单号大于1
   * 取消选中多个Y轴的复选框
   * 更改为栈叠式柱状图
* **[!UICONTROL AOV by quarter]**
   * 量度1 — 收入
      * 隐藏此量度
   * 量度2 — 订单数
      * 隐藏此量度
   * 公式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 量度 — 收入
   * 按客户的`utm_source`分组
* **[!UICONTROL Revenue from top 10 products]**
   * 量度 — 产品收入
      * 隐藏图表
      * 按产品名称分组。 选择所有产品。
      * 将时间范围设置为“全时”
      * 将时间间隔设置为“无”
      * 在“显示排名最前的/最低的”中，仅显示按产品利润排列的排名前10位
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 量度 — 不同的购买者
      * 透视 — 累积
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 会话

通过[!DNL Google Analytics]集成，您可以包括以下报表：

* 网站访问
* 转化率

通过[Commerce数据扩充服务](https://business.adobe.com/products/magento/magento-commerce.html)，您可以包括以下报表：

* 按州/地区、年龄、性别列出的独特客户。

## 其他提示

* 使用简洁明了的[命名约定](../best-practices/naming-elements.md)
* 与投资者用户共享仪表板
* 或通过&#x200B;**[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)发送
* 仅创建一个功能板。 这使内容更容易维护，并且您确切地知道您的投资者在看什么。

周全地组织报告并关注细节。 完成后，功能板将类似于下图：

![构建投资者信息板](../../mbi/assets/investor-dboard-example.png)
