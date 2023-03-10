---
title: 公式
description: 了解如何使用公式。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# 公式

一个公式结合了多个量度和数学逻辑来回答问题。 例如，在假日季节每项产品有多少收入是由新客户产生的？

![仪表板中的假日销售额](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 步骤1：创建基本报表

1. 在菜单中，选择 `Report Builder`.

1. 单击 **[!UICONTROL Add Metric]** 并为报表选择第一个量度。

   在本例中， `Revenue by products ordered` 量度。

1. 单击 **[!UICONTROL Add Metric]** 再次尝试，然后为报表选择第二个量度。

   在本例中， `New Customers` 量度。

1. 在侧栏中，单击 **[!UICONTROL Details]** 以显示有关每个指标的信息。

   ![按订购的产品列出的收入](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. 在侧栏中，单击每个量度的名称，以在新的浏览器选项卡中打开设置页面。 向下滚动查看量度的每个组件，包括量度查询、过滤器和维度。

   ![量度设置](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. 要返回到报表，请单击上一个浏览器选项卡。

1. 在图表中，将鼠标悬停在每行上的几个数据点上，以查看与每个量度关联的数量。

## 步骤2：添加公式

1. 在侧栏顶部，单击 **[!UICONTROL Add Formula]**.

   公式框将量度显示为可用输入 `A` 和 `B`，并包含一个输入框，可在其中输入公式。

   执行以下操作：

   * 在 `Enter your Formul` 输入框，输入 `A/B`.

      这样按新客户数量订购的产品划分收入。

   * 设置 `Select format` 到 `123Number`.

   * 在侧栏中，替换 `Untitled` 具有公式的名称。

   ![公式设置](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完成后，单击 **[!UICONTROL Apply]**.

   报表现在具有公式的新行， `New Customer Revenue`，而侧栏则显示新客户产生的收入总额。

   ![带公式的报表](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 步骤3：添加日期范围

1. 单击 **[!UICONTROL Date Range]** 在右上角。

1. 在 `Fixed Date Range` 选项卡，执行以下操作：

   * 在日历上，选择日期范围。

      例如，假日季节为11月1日至12月31日。

   * 下 `Select Time Interval`，选择 `Day`.

      ![固定日期范围](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完成后，单击 **[!UICONTROL Apply]**.

   现在，报表仅限于假日季节，并且每天都有一个数据点。

   ![固定日期范围](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 步骤4：保存报表

在此步骤中，将报告另存为图表和表格。

1. 单击 `Untitled Report` 并输入描述性标题。 在本例中，报告标题为 `2017 Holiday Sales`.

   然后，执行以下操作：

   * 在右上角，单击 **[!UICONTROL Save]**.

   * 对象 `Type`，接受默认值 `Chart` 设置。

   * 选择 `Dashboard` 在报表可用的位置。

   * 单击 **[!UICONTROL Save to Dashboard]**.

1. 单击报告标题并更改名称。 在本例中，报告标题更改为 `2017 Holiday Sales Data`.

   然后，执行以下操作：

   * 在右上角，单击 **[!UICONTROL Save a Copy]**.

   * 设置 `Type` 到 `Table`.

   * 选择 `Dashboard` 在报表可用的位置。

   * 单击 **[!UICONTROL Save a Copy to Dashboard]**.

1. 要在仪表板中查看报告，请执行下列操作之一：

   * 单击 **[!UICONTROL Go to Dashboard]** 页面顶部的消息中。

   * 在菜单中，选择 **[!UICONTROL Dashboards]**. 单击当前操控板的名称以显示列表。 然后，单击保存报告的功能板名称。
