---
title: 过滤器
description: 了解如何使用过滤器。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 过滤器

可添加一个或多个筛选器以限制用于生成报表的数据。 每个过滤器都是一个表达式，其中包含关联表中的列、运算符和值。 例如，要仅包含回头客户，您可以创建一个仅包含已下多张订单的客户的过滤器。 多个筛选器可以与逻辑`AND/OR`运算符一起使用，以将逻辑添加到报告中。

>[!TIP]
>
>报表最多可以包含3,500个数据点。 要减少数据点的数量，请使用过滤器减少用于生成报表的数据量。

[!DNL Adobe Commerce Intelligence]包括一系列您可以“开箱即用(OOTB)”或根据您的需求修改的筛选器。 您可以创建的过滤器数量没有限制。

## 要添加过滤器，请执行以下操作：

1. 在图表中，将鼠标悬停在每个数据点上。

   在此报表中，每个数据点显示当月客户总数。

1. 在左侧面板中，单击筛选器(![](../../assets/magento-bi-btn-filter.png))图标。

   ![添加筛选器](../../assets/magento-bi-report-builder-filter-add.png)

1. 单击&#x200B;**[!UICONTROL Add Filter]**。

   筛选器按字母顺序编号，第一个是`[A]`。 过滤器的前两个部分是下拉列表选项，第三个部分是值。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 单击过滤器的第一部分，然后选择要用作表达式主体的列。

     ![选择筛选器的第一部分](../../assets/magento-bi-report-builder-filter-part1.png)

   * 单击过滤器的第二部分，然后选择运算符。

     ![选择运算符](../../assets/magento-bi-report-builder-filter-part2.png)

   * 在筛选器的第三部分中，输入完成表达式所需的值。

     ![输入值](../../assets/magento-bi-report-builder-filter-part3.png)

   * 筛选器完成后，单击&#x200B;**[!UICONTROL Apply]**。

     现在，该报表仅包含回头客户，为该报表检索的客户记录数已从33,000减至12,600。

     ![已过滤的报告](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 在侧栏中，单击透视(![](../../assets/magento-bi-btn-perspective.png))图标。

   ![透视](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 在设置列表中选择`Cumulative`。 然后，单击&#x200B;**[!UICONTROL Apply]**。

   ![累积透视](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   `Cumulative`透视会随时间分布变化，而不是显示每个月的锯齿状上下变化。

1. 输入报告的`Title`，然后单击&#x200B;**[!UICONTROL Save]**&#x200B;将其作为`Chart`添加到您的信息板。

   ![保存到仪表板](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
