---
title: 限制量度访问
description: 了解如何使用量度访问和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 管理量度用户

除了设置用户权限级别之外，您还可以根据用户限制对量度的访问。 例如，如果您希望会计部门有权访问与收入相关的量度，但不能访问用户获取量度，则可以限制对这些量度的访问。

在这类情况下，我们建议将该用户的帐户设置为 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 应为不需要创建或更改量度、计算列、集成或用户，但确实需要访问Data warehouse中数据的用户授予权限。 如果要完全限制对数据的访问，请使用 **[!UICONTROL Read Only]** 权限。

设置权限级别后，您可以选择 **[!UICONTROL Standard]** 用户可以通过执行以下操作来访问：

1. 转到 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 选择所需的用户帐户。
1. 的 **[!UICONTROL Metrics]** 选项卡将显示可用量度的列表。 检查您希望用户有权访问的量度；取消选择用户无权访问的用户。
1. [!DNL MBI] 自动保存更改。 如果更改成功， [!DNL MBI] 显示 **[!UICONTROL Saved!]** 的双曲余切值。

>[!NOTE]
>
>具有 **[!UICONTROL Standard]** 权限除了可通过以下方式访问data warehouse中的所有量度之外，还可以通过数据导出来访问 [!DNL Google Analytics].

您还可以通过编辑量度和 **[!UICONTROL Standard]** 在 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 中。

>[!NOTE]
>
>如果复制量度， [!DNL MBI] 复制在原始量度中设置的用户权限。
