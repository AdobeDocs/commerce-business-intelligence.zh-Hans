---
title: 清空您的 [!DNL MBI] 帐户
description: 了解如何清理您的 [!DNL MBI] 帐户。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# 清理您的 [!DNL MBI] 帐户

无论您是否曾与 [!DNL MBI] 在6个月或6年的时间里，保持良好的账户对于贵组织充分利用平台至关重要。 随着时间的推移，用户、功能板、报表、量度和列会自然而然地不再需要。 您可能创建了报表供一次性使用并忘记了该报表，或者离开您公司的用户从未停用过其帐户。

替换为 [对所有元素进行标准化、明确的命名](../best-practices/naming-elements.md)的) [!DNL MBI] 帐户，下面的“帐户审核”步骤可帮助您减少杂乱无章的分析以及对用户的不必要的分析。 一项额外优势包括 [更新周期可能更快](../best-practices/reduce-update-cycle-time.md).

## 步骤1：识别非活动用户

清理帐户的第一步是停用非活动用户的帐户，例如已离开公司或不再使用的用户 [!DNL MBI] 他们目前的角色。

为此，您可以单击顶部导航栏右上角的公司名称，然后选择 **[!UICONTROL Manage Users]**. 接下来，选择要取消激活的用户，然后单击 **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>您需要 [管理员权限](../administrator/user-management/user-management.md) 完成此操作。

>[!WARNING]
>
>停用用户将删除由该用户创建的图表、功能板和其他资源。 如果要保留这些资产，请联系 [!DNL MBI] [支持](../guide-overview.md) 团队名称。 支持人员可以帮助您将这些资源转移给其他用户。

### 重新激活用户

要重新激活用户，请使用已停用的同一电子邮件地址重新创建其帐户，以重新邀请用户，并在登录时恢复其访问及其拥有的数据。

## 步骤2：删除未使用的功能板和报表

审核帐户的下一步是删除任何未使用的功能板和报表。

>[!NOTE]
>
>您需要 `Admin` 或 `Standard` [用户权限](../administrator/user-management/user-management.md) 完成此操作。

每个用户具有 `Admin` 或 `Standard` access可以创建报告和仪表板。 因此，拥有这些权限的所有人都必须执行以下步骤来识别和删除未使用的报表。

### 查看您的仪表板和报告

在删除任何内容之前，您应该查看报告和仪表板，以评估正在使用的内容。 虽然您可以使用 **[!UICONTROL find unused reports]** 任何初始审查都会大大提高清理工作的效率。

### 删除功能板和报表

在访问功能板和报表后，您可以开始清理帐户。

**从功能板中删除报告**

1. 在功能板上找到要删除的报告。
1. 选择 **[!UICONTROL Options]** 报表的右上角。
1. 单击 **[!UICONTROL Remove From Dashboard]**.

**删除整个仪表板**

1. 选择 **[!UICONTROL Manage Data]**，然后**[!UICONTROL Dashboards**].
1. 单击要删除的仪表板。
1. 单击 **[!UICONTROL Delete Dashboard]**.

您还可以选择 **[!UICONTROL Dashboard Options]**，则 **[!UICONTROL Delete]** 从仪表板本身。

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>删除功能板不会删除其中的报表，因此您必须再执行一个步骤来删除报表。

**删除未使用的报告**

1. 选择 **[!UICONTROL Manage Data]**，则 **[!UICONTROL Reports]**.
1. 查看 **仅显示未使用的报表** 框中。 这会创建一个未在功能板或电子邮件摘要中使用的报告列表。
1. 选择要删除的报告。 您可以通过单击报表列表上方的复选框来选择全部。
1. 单击 **[!UICONTROL Delete Selected]**.

以下是未使用的报告删除过程的概况：

![](../../mbi/assets/unused_reports.png)

## 步骤3：删除未使用的量度

清理用户列表、功能板和报告后，您可以开始审核量度列表。 这有助于您识别任何可能已过期或未使用的内容，例如，使用不同的定义创建了一个新量度。

1. 要生成量度的依赖报表列表，请转到 **[!DNL Manage Data]**，然后选择单击 **[!UICONTROL Metrics]**.
1. 单击 **[!UICONTROL Edit]** 在指标旁边。
1. 在页面底部，您会看到一个名为的部分 **[!UICONTROL Dependent Charts]**. 单击该链接可生成此量度的依赖报表列表。
1. 系统完成检查后， [!DNL MBI] 显示使用此量度的功能板、报告和用户的列表。

![](../../mbi/assets/report_dependecies.png)

如果您决定不再需要该量度，请导航回 **[!UICONTROL Metrics]** 页面（通过单击） **[!UICONTROL Back to Metric List]** 以查找要删除的量度。 单击 **[!UICONTROL Delete]**.

## 步骤4：评估已同步的列

最后一步是评估Data warehouse中当前正在同步的列。 取消同步列不仅可以清除您的帐户，还可能会缩短更新时间。

如果您希望实现此目标，请联系 [!DNL MBI] [支持](../guide-overview.md). 支持团队可创建一个报告，该报告应包含任何用户未在任何功能板中使用且未用于电子邮件摘要的所有列（不包括SQL报告）。 然后，您可以使用此报表作为指南，通过Data warehouse管理器选择要取消同步的列。

>[!NOTE]
>
>您以后始终可以再次开始同步这些列。 取消同步列会从Data warehouse中删除任何数据；这仅意味着在更新周期内不会检查此列是否有新值或更新值。

**取消同步列（或列）**

1. 转到 **[!DNL Manage Data]**，则 **[!UICONTROL Data Warehouse]**.
1. 在 **[!UICONTROL Synced Tables]** 列表时，导航到包含该列的表。
1. 选中要取消同步的一个或多个列旁边的一个或多个框。
   >[!NOTE]
   >
   >如果不删除整个表，则无法取消同步主键列。

1. 单击 **[!UICONTROL Remove]** 以取消同步一个或多个列。

下面我们来看看整个过程：

![](../../mbi/assets/drop_column.png)

## 总结

就是这样！ 您的 [!DNL MBI] 现在，帐户应该更整洁，更便于您和您的团队导航。
