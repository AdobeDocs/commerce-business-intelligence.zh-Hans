---
title: 为量度创建过滤器集
description: 了解如何创建保存的过滤器集并将它们应用于量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 创建过滤器集

如果您在中拥有多个量度 [!DNL Commerce Intelligence] （例如，过滤掉测试订单）的过滤条件，您可以创建保存的过滤器集并将它们应用于量度。 这样可节省您的时间，因为在创建或编辑量度时您不必添加单个过滤器。

请参阅 [训练视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) 以了解更多信息。

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

1. 单击 **[!DNL Manage Data** > **Filter Sets]** 在侧栏中。

   ![](../../assets/create-filter-sets.png)

1. 单击 **[!UICONTROL Add Filter Set]** 页面顶部的。

1. 选择包含要过滤的量度的表。

   例如，如果要筛选 `Total number of orders` 量度，并且它构建于 `orders` 表，选择该表。

1. 为命名 `Filter Set`.

1. 添加所有相关筛选器。

   例如，如果您只想在 `Total number of orders` 量度，您将应用一个过滤器，以排除所有没有状态的订单= `complete`.

1. 验证筛选条件逻辑以及括号和运算符是否已正确放置：例如， `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   不正确的筛选器通常是导致两者之间存在数据差异的原因 [!DNL Commerce Intelligence] 报告和预期结果。

1. 保存 `Filter Set`.

保存过滤器集后，您可以将其应用于使用同一表的任何量度。 例如，如果您创建 `Filter Set` 在 `orders` 表格，您可以将其应用于 *任何量度* 构建在此表格之上，例如 `Revenue`.

>[!NOTE]
>
>`Filter Sets` 也可以应用于中的计算列 [!DNL Commerce Intelligence]. 您可以请求将过滤器集应用于在中创建的数据维度 [!DNL Commerce Intelligence] 通过联系支持人员。

## 相关

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
