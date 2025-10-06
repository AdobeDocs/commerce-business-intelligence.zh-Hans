---
title: 清空您的 [!DNL Commerce Intelligence] 帐户
description: 了解如何清理 [!DNL Commerce Intelligence] 帐户。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 清理[!DNL Adobe Commerce Intelligence]帐户

无论您已经与[!DNL Commerce Intelligence]合作六个月还是六年，保持良好的帐户对于您的组织充分利用平台至关重要。 随着时间的推移，用户、功能板、报表、量度和列自然而然地不再需要。 您可能创建了报表供一次性使用并忘记了该报表，或者离开您公司的用户从未停用过其帐户。

通过[帐户的所有元素](../best-practices/naming-elements.md))的[!DNL Commerce Intelligence]标准化、清晰的命名，以下帐户审核步骤可帮助您减少用户的混乱和不必要的分析。 另一个优势包括[可能更快的更新周期](../best-practices/reduce-update-cycle-time.md)。

## 步骤1：识别非活动用户

清理帐户的第一步是停用非活动用户的帐户，例如已离开公司或不再在其当前角色中使用[!DNL Commerce Intelligence]的用户。

为此，请单击右上角导航栏中您公司的名称，然后选择&#x200B;**[!UICONTROL Manage Users]**。 接下来，选择要取消激活的用户并单击&#x200B;**[!UICONTROL Deactivate User]**。

>[!NOTE]
>
>您需要[管理员权限](../administrator/user-management/user-management.md)才能执行此操作。

>[!WARNING]
>
>停用用户将删除由该用户创建的图表、功能板和其他资源。 如果要保留这些资产，请在停用用户之前联系[!DNL Commerce Intelligence] [支持](../guide-overview.md#Submitting-a-Support-Ticket)团队。 支持人员可以帮助您将这些资源转移给其他用户。

### 重新激活用户

要重新激活用户，请使用已停用的同一电子邮件地址重新创建其帐户，以重新邀请用户，并在登录时恢复其访问及其拥有的数据。

## 第2步：删除未使用的功能板和报表

审核帐户的下一步是删除任何未使用的功能板和报表。

>[!NOTE]
>
>您需要`Admin`或`Standard` [用户权限](../administrator/user-management/user-management.md)才能执行此操作。

每个具有`Admin`或`Standard`访问权限的用户都可以创建报告和仪表板。 因此，拥有这些权限的每个人必须按照以下步骤识别和删除未使用的报表。

### 查看您的仪表板和报告

在删除任何内容之前，您应该查看报告和仪表板以评估正在使用的内容。 虽然您可以使用下面描述的&#x200B;**[!UICONTROL find unused reports]**&#x200B;功能，但任何初始审查都会使您的清理工作更高效。

### 删除功能板和报表

访问功能板和报表后，即可开始清理帐户。

**从仪表板删除报告**

1. 在功能板上找到要删除的报告。
1. 选择报告右上角的&#x200B;**[!UICONTROL Options]**。
1. 单击&#x200B;**[!UICONTROL Remove From Dashboard]**。

**删除整个仪表板**

1. 选择&#x200B;**[!UICONTROL Manage Data]**，然后选择**[!UICONTROL Dashboards**]。
1. 单击要删除的仪表板。
1. 单击&#x200B;**[!UICONTROL Delete Dashboard]**。

您还可以从仪表板本身选择&#x200B;**[!UICONTROL Dashboard Options]**，然后选择&#x200B;**[!UICONTROL Delete]**。

![删除仪表板齿轮菜单中的选项](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>删除功能板不会删除其中的报表，因此您必须再执行一个步骤来删除报表。

**删除未使用的报告**

1. 选择&#x200B;**[!UICONTROL Manage Data]**，然后选择&#x200B;**[!UICONTROL Reports]**。
1. 选中位于量度列表下方的&#x200B;**仅显示未使用的报表**&#x200B;框。 这会创建一个未在功能板或电子邮件摘要中使用的报告列表。
1. 选择要删除的报告。 您可以通过单击报表列表上方的复选框来选择全部。
1. 单击&#x200B;**[!UICONTROL Delete Selected]**。

以下是未使用的报告删除流程概况：

![未使用的报告列表显示不在任何仪表板上的报告](../../mbi/assets/unused_reports.png)

## 步骤3：删除未使用的量度

清理用户列表、功能板和报告后，您可以转到审核量度列表。 这有助于您识别任何可能已过期或未使用的内容，例如，使用不同的定义创建了一个新量度。

1. 要生成量度的依赖报表列表，请转到&#x200B;**[!DNL Manage Data]**，然后选择“单击&#x200B;**[!UICONTROL Metrics]**”。
1. 单击量度旁边的&#x200B;**[!UICONTROL Edit]**。
1. 在页面底部，您会看到名为&#x200B;**[!UICONTROL Dependent Charts]**&#x200B;的部分。 单击该链接可生成此度量的依赖报表列表。
1. 系统完成检查后，[!DNL Commerce Intelligence]会显示使用此量度的功能板、报告和用户的列表。

![报告依赖关系对话框，显示哪些报告使用所选列](../../mbi/assets/report_dependecies.png)

如果您决定不再需要该量度，请单击&#x200B;**[!UICONTROL Metrics]**&#x200B;以导航回&#x200B;**[!UICONTROL Back to Metric List]**&#x200B;页面，查找要删除的量度。 单击&#x200B;**[!UICONTROL Delete]**。

## 步骤4：评估已同步的列

最后一步是评估Data Warehouse中当前正在同步的列。 取消同步列不仅可以清除您的帐户，还可能会缩短更新时间。

如果您想追求此目标，请联系[!DNL Commerce Intelligence] [支持](../guide-overview.md#Submitting-a-Support-Ticket)。 支持团队可以创建报告，该报告包含任何用户未在任何仪表板中使用以及电子邮件摘要（不包括SQL报告）中未使用的所有列。 然后，您可以使用此报表作为指南，指导您通过Data Warehouse Manager选择要取消同步的列。

>[!NOTE]
>
>您以后始终可以再次开始同步这些列。 取消同步列将从Data Warehouse中删除任何数据；这仅意味着在更新周期内不会检查此列是否有新值或更新值。

**取消同步列（或列）**

1. 转到&#x200B;**[!DNL Manage Data]**，然后转到&#x200B;**[!UICONTROL Data Warehouse]**。
1. 在&#x200B;**[!UICONTROL Synced Tables]**&#x200B;列表中，导航到包含该列的表。
1. 选中要取消同步的一个或多个列旁边的一个或多个框。

   >[!NOTE]
   >
   >如果不删除整个表，则无法取消同步主键列。

1. 单击&#x200B;**[!UICONTROL Remove]**&#x200B;取消同步一个或多个列。

下面是整个过程的概况：

Data Warehouse Manager中的![删除列选项](../../mbi/assets/drop_column.png)

## 正在结束

对于您和您的团队，您的[!DNL Commerce Intelligence]帐户现在应该更整洁且更易于导航。
