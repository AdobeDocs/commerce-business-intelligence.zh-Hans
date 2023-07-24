---
title: 限制指标访问
description: 了解如何使用指标访问和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 管理指标用户

除了设置用户权限级别之外，您还可以按用户限制对量度的访问。 例如，如果您希望会计部门可以访问与收入相关的指标，但不能访问用户获取指标，则可以限制对这些指标的访问。

在这种情况下，Adobe建议将该用户帐户设置为 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 应该向不需要创建或更改量度、计算列、集成或用户的用户授予权限，但是他们确实需要访问Data warehouse中的数据。 如果要完全限制对数据的访问，请使用 **[!UICONTROL Read Only]** 权限。

设置权限级别后，您可以选择指标 **[!UICONTROL Standard]** 用户可通过以下方式访问：

1. 转到 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 选择所需的用户帐户。
1. 此 **[!UICONTROL Metrics]** 选项卡显示可用度量的列表。 选中您希望用户有权访问的量度，并取消选择用户不应有权访问的量度。
1. [!DNL Adobe Commerce Intelligence] 自动保存更改。 如果更改成功， [!DNL Commerce Intelligence] 显示 **[!UICONTROL Saved!]** 页面顶部的。

>[!NOTE]
>
>所有用户具有 **[!UICONTROL Standard]** 除了来自的所有量度之外，权限还可以通过“数据导出”访问Data warehouse中的所有数据 [!DNL Google Analytics].

您还可以通过编辑量度和 **[!UICONTROL Standard]** 在中选择用户 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 部分。

>[!NOTE]
>
>如果复制量度， [!DNL Commerce Intelligence] 复制在原始量度中设置的用户权限。
