---
title: 限制指标访问
description: 了解如何使用量度访问和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b6935462-7263-4ced-a703-60de6a5aeb2d
subfeature_v2: id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: efc8727dd67a9ffcd7a8a1059ea93df8c6344599
workflow-type: tm+mt
source-wordcount: 242
ht-degree: 0%

---

# 管理指标用户

除了设置用户权限级别之外，您还可以按用户限制对量度的访问。 例如，如果您希望会计部门可以访问与收入相关的指标，但不可以访问用户获取指标，则可以限制对这些指标的访问。

在这种情况下，Adobe建议将该用户帐户设置为&#x200B;**[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**。 应该向不需要创建或更改指标、计算列、集成或用户的用户授予&#x200B;**[!UICONTROL Standard]**&#x200B;权限，但是他们确实需要访问Data Warehouse中的数据。 如果要完全限制对数据的访问，请改用&#x200B;**[!UICONTROL Read Only]**&#x200B;权限。

在设置权限级别后，您可以通过执行以下操作选择&#x200B;**[!UICONTROL Standard]**&#x200B;用户可以访问的量度：

1. 转到&#x200B;**[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**。
1. 选择所需的用户帐户。
1. **[!UICONTROL Metrics]**&#x200B;选项卡显示可用量度的列表。 选中您希望用户有权访问的量度，并取消选择用户不应有权访问的量度。
1. [!DNL Adobe Commerce Intelligence]自动保存更改。 如果更改成功，[!DNL Commerce Intelligence]会在页面顶部显示&#x200B;**[!UICONTROL Saved!]**。

>[!NOTE]
>
>除了来自[!DNL Google Analytics]的所有量度之外，所有具有&#x200B;**[!UICONTROL Standard]**&#x200B;权限的用户还可以通过“数据导出”访问Data Warehouse中的所有数据。

您还可以通过编辑量度并在&#x200B;**[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**&#x200B;部分中选择&#x200B;**[!UICONTROL Standard]**&#x200B;用户来限制对量度的访问。

>[!NOTE]
>
>如果您复制了一个量度，[!DNL Commerce Intelligence]将复制原始量度中设置的用户权限。

