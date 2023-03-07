---
title: 管理数据维度
description: 了解维度是什么，它可用于根据量度过滤或划分图表。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 管理数据维度

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

维度是同一表中作为量度的字段，可用于根据该量度过滤或划分图表。 例如，收入量度可能包含城市、州/省、国家/地区、订单状态、优惠券代码和其他类型的维度。

## 将维度添加到多个量度

要一次将一个或多个维度添加到多个量度，请执行以下操作：

1. 在主导航栏上，转到 **[!UICONTROL Manage Data > Metrics]**.

1. 在页面顶部，单击 **[!UICONTROL Add Dimensions To Metric(s)]**.

1. 选择包含维度的表。

1. 在 `Choose Metric(s) to Add Dimensions` 列中，选择要将维度添加到的量度。 一旦选定， `Choose Dimensions to Add` 列显示在右侧。 选中要添加到所选量度的维度。

   ![](../../assets/Add_Dimensions.png)

1. 如果要按报表中的任何数据维度进行分段或分组，请确保指出它们是 _可分组_.

1. 单击 **[!UICONTROL Add]**.

## 从多个量度中删除维度

要从多个量度中删除一个或多个维度，请执行以下操作：

1. 在主导航栏上，转到 **[!UICONTROL Data > Metrics]**.

1. 在页面顶部，单击 **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. 选择包含维度的表。

1. 在左侧选择要删除维度的量度，并在右侧选择要删除的维度。

1. 单击 **[!UICONTROL Remove]**.

1. 如果维在报表中使用，您会看到警告和使用维的图表列表。 单击 **[!UICONTROL Delete]** 删除选中的维及其所有从属项，包括报表。

## 管理量度中的维度

**要在量度中添加维度，请执行以下操作：**

1. 在主导航栏上，转到 **[!UICONTROL Data > Metrics]**.

1. 单击 **[!UICONTROL Edit]** 在需要新维度的量度上。

1. 在 `Dimensions` 部分，使用 `Add a dimension` 下拉菜单以选择要添加的维度。

>[!NOTE]
>
>必须已在中跟踪您要过滤或分组的任何维度 [!DNL MBI]. 如果找不到所需的维度，您可能需要开始通过 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 页面。


**要从量度中删除维度，请执行以下操作：**

1. 在主导航栏上，转到 **[!UICONTROL Manage Data > Metrics]**.

1. 单击 **[!UICONTROL Edit]** 在需要新维度的量度上。

1. 在 `Dimensions` 部分，选中要删除的维度旁边的“删除”列中的复选框。

>[!NOTE]
>
>即使删除某个维度后，它仍作为Data warehouse中表上的列存在。 您可以将其添加回任何量度，并使用这些维度构建新量度。 从删除与维度对应的数据列 [!DNL MBI]，只需通过 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 页面。

## 相关文档

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
