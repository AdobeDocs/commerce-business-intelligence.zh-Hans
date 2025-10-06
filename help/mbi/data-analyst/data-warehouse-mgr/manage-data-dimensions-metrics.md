---
title: 管理数据维度
description: 了解维度是什么，它可用于根据量度过滤或划分图表。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 管理数据维度

>[!NOTE]
>
>需要[管理员权限](../../administrator/user-management/user-management.md)。

维度是同一表中作为量度的字段，可用于根据该量度过滤或划分图表。 例如，收入量度可能包含城市、州/省、国家/地区、订单状态、优惠券代码和其他类型的维度。

## 将维度添加到多个量度

要一次将一个或多个维度添加到多个量度，请执行以下操作：

1. 转到&#x200B;**[!UICONTROL Manage Data > Metrics]**。

1. 单击&#x200B;**[!UICONTROL Add Dimensions To Metric(s)]**。

1. 选择包含维度的表。

1. 在`Choose Metric(s) to Add Dimensions`列中，选择要将维度添加到的量度。 选定后，`Choose Dimensions to Add`列将显示在右侧。 选中要添加到所选量度的维度。

   ![添加维度对话框，显示可用的维度选项](../../assets/Add_Dimensions.png)

1. 如果要按报表中的任何数据维度进行分段或分组，请确保指示它们是&#x200B;_可分组的_。

1. 单击&#x200B;**[!UICONTROL Add]**。

## 从多个量度中删除维度

要从多个量度中删除一个或多个维度，请执行以下操作：

1. 转到&#x200B;**[!UICONTROL Data > Metrics]**。

1. 单击&#x200B;**[!UICONTROL Remove Dimensions From Metric(s)]**。

1. 选择包含维度的表。

1. 选择您要从左侧删除维度的量度，以及您要从右侧删除的维度。

1. 单击&#x200B;**[!UICONTROL Remove]**。

1. 如果维正在报表中使用，则警告将显示使用这些维的图表列表。 单击&#x200B;**[!UICONTROL Delete]**&#x200B;可删除选中的维度及其所有依赖项，包括报表。

## 管理量度中的维度

**在量度中添加维度：**

1. 转到&#x200B;**[!UICONTROL Data > Metrics]**。

1. 在需要新维度的量度上单击&#x200B;**[!UICONTROL Edit]**。

1. 在`Dimensions`部分中，使用`Add a dimension`下拉菜单选择要添加的维度。

>[!NOTE]
>
>必须在[!DNL Commerce Intelligence]中跟踪您要过滤或分组依据的任何维度。 如果找不到所需的维度，您可能需要通过[Data Warehouse](../data-warehouse-mgr/tour-dwm.md)页面开始跟踪数据库中的新数据列。


**要从量度中删除维度：**

1. 转到&#x200B;**[!UICONTROL Manage Data > Metrics]**。

1. 在需要新维度的量度上单击&#x200B;**[!UICONTROL Edit]**。

1. 在`Dimensions`部分下，选中要删除的维度旁边的删除列中的复选框。

>[!NOTE]
>
>即使删除某个维度后，它仍作为Data Warehouse中表上的列存在。 您可以将其添加回任何量度，并使用这些维度构建新量度。 要从[!DNL Commerce Intelligence]中删除维度对应的数据列，只需通过[Data Warehouse](../data-warehouse-mgr/tour-dwm.md)页面取消跟踪该数据列即可。

## 相关文档

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
