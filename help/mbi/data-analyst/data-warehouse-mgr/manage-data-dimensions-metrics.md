---
title: 管理数据维度
description: 了解数据的生成方式、新行插入其中一个核心商务的确切原因，以及购买或创建帐户等操作如何记录到商务数据库中。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 管理数据维度

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

维度是同一表中的字段，用于根据该量度过滤或划分图表。 例如，收入量度可能包含城市、州、国家/地区、订单状态、优惠券代码和其他类型的维度。

## 将维度添加到多个量度

要一次将一个或多个维度添加到多个量度，请执行以下操作：

1. 在主导航栏上，转到 **[!UICONTROL Manage Data > Metrics]**.

1. 在页面顶部，单击 **[!UICONTROL Add Dimensions To Metric(s)]**.

1. 选择包含维的表。

1. 在 `Choose Metric(s) to Add Dimensions` 列中，选择要将维度添加到的量度。 选择后， `Choose Dimensions to Add` 列将显示在右侧。 选中要添加到选定量度的维度。

   ![](../../assets/Add_Dimensions.png)

1. 如果要按报表上的任何数据维度进行分段或分组，请确保指明它们是 _可分组_.

1. 单击 **[!UICONTROL Add]**.

## 从多个量度中删除维度

要从多个量度中删除一个或多个维度，请执行以下操作：

1. 在主导航栏上，转到 **[!UICONTROL Data > Metrics]**.

1. 在页面顶部，单击 **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. 选择包含维的表。

1. 选择要从左侧删除维度的量度，以及要在右侧删除的维度。

1. 单击 **[!UICONTROL Remove]**.

1. 如果维度在报表上使用，将显示一条警告消息和使用维度的图表列表。 单击 **[!UICONTROL Delete]** 删除选中的维度及其所有依赖项（包括报表）。

## 管理量度中的维度

**要在量度中添加维度，请执行以下操作：**

1. 在主导航栏上，转到 **[!UICONTROL Data > Metrics]**.

1. 单击 **[!UICONTROL Edit]** 量度上的。

1. 在 `Dimensions` 部分，使用 `Add a dimension` 下拉列表以选择要添加的维度。

>[!NOTE]
>
>您要按进行筛选或分组的任何维度必须已在 [!DNL MBI]. 如果找不到所需的维度，我们可能需要通过 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 页面。


**要从量度中删除维度，请执行以下操作：**

1. 在主导航栏上，转到 **[!UICONTROL Manage Data > Metrics]**.

1. 单击 **[!UICONTROL Edit]** 量度上的。

1. 在 `Dimensions` 部分中，选中要删除的维度旁边删除列中的复选框。

>[!NOTE]
>
>即使删除某个维度后，它仍作为列存在于我们的data warehouse中。 您可以将其添加回任何量度，并使用这些维度构建新量度。 要从中删除与对应的维度的数据列，请执行以下操作 [!DNL MBI]，只需通过 [data warehouse](../data-warehouse-mgr/tour-dwm.md) 页面。

## 相关文档

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
