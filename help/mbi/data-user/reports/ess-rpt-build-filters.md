---
title: 过滤器
description: 了解如何使用过滤器。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 过滤器

可添加一个或多个过滤器以限制用于生成报表的数据。 每个过滤器都是一个表达式，其中包含来自关联表的列、运算符和值。 例如，要仅包含重复客户，您可以创建一个过滤器，该过滤器仅包含已下多个订单的客户。 多个过滤器可与逻辑 `AND/OR` 运算符将逻辑添加到报表。

>[!TIP]
>
>一个报表最多可以有3,500个数据点。 要减少数据点数，请使用过滤器减少用于生成报表的数据量。

MBI包含一系列筛选器，您可以使用“开箱即用”(OOTB)或根据需要进行修改。 您可以创建的过滤器数量没有限制。

## 添加过滤器：

1. 在图表中，将鼠标悬停在每个数据点上。

   在此报表中，每个数据点都显示当月的客户总数。

1. 在左侧面板中，单击“Filters（过滤器）”(![](../../assets/magento-bi-btn-filter.png))图标。

   ![添加过滤器](../../assets/magento-bi-report-builder-filter-add.png)

1. 单击 **[!UICONTROL Add Filter]**.

   过滤器按字母顺序编号，第一个按 `[A]`. 过滤器的前两个部分是下拉选项，第三个部分是一个值。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 单击过滤器的第一部分，然后选择要用作表达式主题的列。

      ![选择过滤器的第一部分](../../assets/magento-bi-report-builder-filter-part1.png)

   * 单击过滤器的第二部分并选择运算符。

      ![选择运算符](../../assets/magento-bi-report-builder-filter-part2.png)

   * 在过滤器的第三部分，输入完成表达式所需的值。

      ![输入值](../../assets/magento-bi-report-builder-filter-part3.png)

   * 过滤器完成后，单击 **[!UICONTROL Apply]**.

      报表现在仅包含重复客户，并且为报表检索的客户记录数已从3.3万减少到1.26万。

      ![过滤的报表](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 在侧栏中，单击透视( ![](../../assets/magento-bi-btn-perspective.png))图标。

   ![透视](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 在设置列表中，选择 `Cumulative`. 然后，单击 **[!UICONTROL Apply]**.

   ![累积视角](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   的 `Cumulative` 透视图可分布随时间的变化，而不是显示每月的起伏。

1. 输入 `Title` ，然后单击 **[!UICONTROL Save]** a `Chart` 功能板。

   ![保存到功能板](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
