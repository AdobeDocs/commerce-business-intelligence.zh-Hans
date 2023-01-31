---
title: 为投资者构建仪表板
description: 了解如何为投资者构建仪表板。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 构建投资者仪表板

我们的许多客户都在与投资者合作，需要与他们共享平台中的信息，但是您创建的用于做出日常业务决策的功能板，可能不是投资者想要的。 在此，我们介绍了一些有关如何创建功能板的最佳实践，该功能板全面而简单，非常适合与活跃的潜在投资者共享。

以下是为投资者仪表板创建报告所需的内容：

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
   * 过滤器 — 用户的订单编号等于1
   * 量度2 — 重复订单收入
      * 过滤器 — 用户的订单号大于1
   * 取消选中多个Y轴的框
   * 更改堆叠式列图
* **[!UICONTROL AOV by quarter]**
   * 量度1 — 收入
      * 隐藏此量度
   * 量度2 — 订购数
      * 隐藏此量度
   * 公式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 量度 — 收入
   * 按客户的 `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 量度 — 产品收入
      * 隐藏图表
      * 按产品名称分组。 选择所有产品。
      * 将时间范围设置为“全时”
      * 将时间间隔设置为“无”
      * 在“显示顶部/底部”中，仅显示按产品利润排序的前10个
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 量度 — 独特购买者
      * 透视 — 累积
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 会话

使用 [!DNL Google Analytics] 集成时，您可以包含以下报表：

* 网站访问量
* 转化率

使用 [商务数据扩充服务](https://business.adobe.com/products/magento/magento-commerce.html)，则可以包含以下报表：

* 按州/地区、年龄、性别划分的独特客户。

## 其他提示

* 简洁明了 [命名约定](../best-practices/naming-elements.md)
* 与投资者用户共享功能板
* 或通过 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 仅创建一个功能板。 这将使内容更易于维护，并且您将确切了解您的投资者正在查看的内容。

周密地组织报告并注意细节。 完成后，功能板将类似于以下内容：

![](../../mbi/assets/investor-dboard-example.png)
