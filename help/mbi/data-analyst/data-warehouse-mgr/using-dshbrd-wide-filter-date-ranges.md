---
title: 功能板范围筛选
description: 了解如何在特定仪表板上批量编辑所有报告。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 功能板范围筛选

通过功能板范围的筛选，您可以对特定功能板上的所有报告进行批量编辑。 您可以快速查看不同时间段或不同商店的相同分析。 您可以轻松地比较每个商店去年、月或周的性能。 您可以更新整个仪表板以适应新启动的活动。

## 日期过滤器

要更改功能板上报告的日期范围或时间间隔，请单击右上角的日历图标(![日历](../../assets/calendar-button.png))。

您可以选择使用查看数据 `Fixed Date Range` 或各种预先计算的 `Moving Date Ranges`：

![移动日期范围](../../assets/moving_date_ranges.png)

此 `Last Full...` 移动范围选项表示最近完全完成的范围，而 `This...` 是当前正在进行的范围。 例如，如果现在是六月， `Last Full Month` 是 _5月1日 — 5月31日_，而 `This Month` 是 _6月1日至现在_.

或者创建您自己的 `Custom Moving Range`\：

![自定义移动范围](../../assets/custom-moving-range.png)

选择以更改间隔。 选择默认按钮(![时间间隔默认值](../../assets/time_interval_default.png))表示只有日期范围会更改：

![时间间隔](../../assets/time_interval.png)

要将所有报告恢复到其初始日期范围和时间间隔，请单击 **[!UICONTROL Restore Defaults]** 或单击 **[!UICONTROL Cancel]**.

为功能板指定日期过滤器时，该过滤器仅应用于该功能板。 当您导航到其他功能板时，不会应用此功能。

>[!NOTE]
>
>目前， `Cohort Reports` 和 `SQL Reports` 在功能板级别应用更改时不包含。

## 存储筛选器

要分析特定商店的执行情况，请单击右上角的商店图标(![商店筛选条件](../../assets/store-filter.png))。 默认情况下， `Store Filter` 设置为 `All Stores`，其中显示来自所有 [商店视图](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) 在您的Commerce网站中提供。

>[!NOTE]
>
>商店筛选器已针对整个网站启用或禁用 [!DNL Commerce Intelligence] 帐户。 如果功能板包含不受过滤器影响的报表（例如未在任何功能板的基础上构建报表） [!DNL Adobe Commerce] 数据)，则应用商店筛选条件时，这些报表不会更新。 您可以 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果您认为报表应基于存储选择进行更新，或者如果您认为您的帐户存储过滤器被错误地禁用。

当您从中选择商店时 `Store Filter`，则当您在功能板之间导航时，过滤器会保留您的选择。 保留您的选择允许您查看所选存储中任何位置的数据，直到您选择为止 `All Stores`.

## 共享功能板的筛选器

对于共享功能板，如果一位用户配置日期过滤器，则具有该功能板访问权限的其他用户会看到应用了该同一过滤器。 但是，存储过滤器不适用于这种情况。 如果功能板所有者配置商店筛选条件并共享功能板，则配置的商店筛选条件不会保留给其他用户。 用户必须具有 [编辑访问权限](../../data-user/dashboards/share-dashboard-with-users.md) ，以调整功能板筛选器。
