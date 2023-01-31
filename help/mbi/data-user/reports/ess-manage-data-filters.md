---
title: 为量度创建过滤器集
description: 了解如何创建保存的过滤器集并将其应用于量度。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 创建过滤器集

如果您在 [!DNL MBI] 需要以类似方式过滤的过滤器（例如，过滤掉测试订单），您可以创建保存的过滤器集并将其应用于量度。 这样可节省您的时间，因为在创建或编辑量度时，您无需添加单个过滤器。

查看我们的 [培训视频](https://support.magento.com/hc/en-us/articles/360016730151) 以了解更多。

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

1. 单击 **[!DNL Manage Data** > **Filter Sets]** 中。

   ![](../../assets/create-filter-sets.png)

1. 单击 **[!UICONTROL Add Filter Set]** 的双曲余切值。

1. 选择包含要过滤的量度的表。

   例如，如果要过滤 `Total number of orders` 量度，并且它基于 `orders` 表格，选择该表格。

1. 将 `Filter Set`.

1. 添加所有相关过滤器。

   例如，如果我们只想在 `Total number of orders` 量度时，我们会应用一个过滤器，该过滤器将排除所有没有状态= `complete`.

1. 验证过滤器逻辑，以及括号和运算符的放置是否正确：例如， `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   错误的过滤器通常是 [!DNL MBI] 报告和预期结果。

1. 保存 `Filter Set`.

保存过滤器集后，您可以将其应用于使用同一表的任何量度。 例如，如果您创建了 `Filter Set` 在 `orders` 表格，可将其应用到 *任何量度* 构建于此表，例如 `Revenue`.

>[!NOTE]
>
>`Filter Sets` 也可应用于 [!DNL MBI]. 您可以请求将过滤器集应用到在中创建的数据维度 [!DNL MBI] 通过联系支持人员。

## 相关

* [分段和过滤的最佳实践](../../best-practices/segment-filter.md)
