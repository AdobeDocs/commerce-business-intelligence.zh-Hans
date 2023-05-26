---
title: 为量度创建过滤器集
description: 了解如何创建保存的过滤器集并将其应用于量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 创建过滤器集

如果您在中拥有多个量度 [!DNL Commerce Intelligence] （例如，过滤掉测试订单）时，您可以创建保存的过滤器集并将它们应用于量度。 这节省了您的时间，因为在创建或编辑量度时您不必添加单个过滤器。

请参阅 [训练视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) 了解更多信息。

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

1. 单击 **[!DNL Manage Data** > **Filter Sets]** 在侧栏中。

   ![](../../assets/create-filter-sets.png)

1. 单击 **[!UICONTROL Add Filter Set]** 页面顶部的。

1. 选择包含要过滤的量度的表。

   例如，如果要筛选 `Total number of orders` 量度且构建于 `orders` 表，请选择该表。

1. 命名 `Filter Set`.

1. 添加所有相关筛选器。

   例如，如果您只想在 `Total number of orders` 量度时，您将应用一个过滤器，以排除所有没有状态的订单= `complete`.

1. 验证筛选条件逻辑以及括号和运算符的放置是否正确：例如， `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   不正确的筛选器通常是造成两者之间数据不一致的原因 [!DNL Commerce Intelligence] 报告和您的预期结果。

1. 保存 `Filter Set`.

保存过滤器集后，您可以将其应用于使用同一表的任何量度。 例如，如果您创建了 `Filter Set` 在 `orders` 表，您可以将其应用于 *任意量度* 构建在此表格之上，例如 `Revenue`.

>[!NOTE]
>
>`Filter Sets` 也可以应用于中的计算列 [!DNL Commerce Intelligence]. 您可以请求将过滤器集应用到在中创建的数据维度 [!DNL Commerce Intelligence] 通过联系支持人员。

## 相关

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
