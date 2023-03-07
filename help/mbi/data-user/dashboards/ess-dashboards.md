---
title: 仪表板
description: 了解如何创建和使用功能板。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 仪表板

[!DNL MBI] 功能板可让您一目了然地快速查看商店的绩效和销售活动。 单个功能板可以与其他用户共享，并组织到逻辑组中。 您还可以为其他用户设置不同级别的权限。

可以轻松创建报表、将其添加到功能板，以及将数据导出到Excel。 可以调整图表和报告的大小，并将其拖动到功能板上的适当位置。

![仪表板](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 创建功能板 {#createdash}

功能板是可共享的，用于您在Report Builder中创建的分析的主题桶。 这就是您如何鼓励您的团队进行协作并在整个组织中维护单一真实来源的方法。

*如果您是管理员或标准用户*，您可以通过单击 `Dashboard Options` 下拉列表和选择 `Create New dashboard`.

您创建的功能板是什么样的，完全取决于您。 您可以根据需要和工作流程在功能板中以任何方式排列元素并调整其大小。

![排列调整仪表板元素大小](../../assets/arrange_resize_dashboard_element.gif)

### 创建功能板

1. 在菜单上，单击 **[!UICONTROL Dashboards]**.

1. 默认仪表板的名称显示在仪表板标题的左上角。 单击向下箭头(![](../../assets/magento-bi-btn-down.png))以显示可用选项。

   ![创建功能板](../../assets/magento-bi-dashboard-create.png)

1. 单击 **[!UICONTROL Create Dashboard]**. 然后，执行以下操作：

   * 输入 `Name` 您的信息板的。

   * 创建 `Group` 对于仪表板，输入组的名称。

      例如，如果您的Commerce安装有多个商店视图，则可以为每个商店视图创建一个组。

   * 单击 **[!UICONTROL Create]**.

   ![仪表板名称](../../assets/magento-bi-dashboard-create-name.png)

   * 新仪表板的名称将显示在左上角。 单击向下箭头(![](../../assets/magento-bi-btn-down.png))以显示选项。 如果创建了组，则新仪表板将显示在列表中该组的下方。


### 添加报告

1. 要添加报告，请执行以下操作之一：

   * 单击 **[!UICONTROL Add a report]** 提示符。

   * 在功能板标题中，单击 **[!UICONTROL Add Report]**.

      ![添加报告](../../assets/magento-bi-dashboard-create-add-report.png)

1. 单击 **[!UICONTROL Create Report]** 以显示 **[!UICONTROL Report Builder Options]**.

   ![Report Builder选项](../../assets/magento-bi-report-builder.png)

## 在仪表板上排列项目

* 要调整图表或报表的大小，请将右下角拖动到新大小。

* 要移动图表或报表，请将光标悬停在标题或标题上，直到光标变为十字形。 然后，将其拖动到相应位置。

## 管理功能板 {#managedash}

In **[!DNL Manage Data** > **Dashboards]**，您可以管理自己拥有的仪表板的用户权限，删除不再需要的仪表板，以及设置默认仪表板。

### 共享您的仪表板 {#sharingdash}

实现真正规模化 [!DNL MBI] 在整个组织并提供有价值的见解后，Adobe鼓励您与其他团队成员共享您创建的功能板。 *您可以共享您拥有的仪表板* 单击 `Share Dashboard` 选项。

当您共享功能板时，您可以跨组织或单独分配权限，这意味着您可以决定谁可以查看和编辑报表。

>[!NOTE]
>
>`Read-Only` 用户只能访问与他们直接共享的仪表板 — 他们无法自行搜索和添加仪表板。 别忘了把它们关在圈子里！

### 访问共享功能板 {#accessshared}

*如果您是管理员或标准用户* 并想要向帐户添加共享功能板，您可以通过单击 **[!UICONTROL Dashboard Options]** 然后单击 **[!UICONTROL Find]** 在下拉菜单中。

![查找仪表板](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 管理功能板设置

1. 在菜单上，单击 **[!DNL Manage Data** > **Dashboards]**.

1. 如果适用，请输入新的 `Dashboard Name`.

1. 将功能板分配给特定 `Dashboard Group`，从组列表中选择。

   **`Permissions`**

   要向所有用户授予对功能板的相同级别的访问权限，请执行以下操作：

   1. 下 **`Shared with`**，请选择以下选项之一：

      * `View`
      * `Edit`
      * `None`
   1. 提示确认时，单击 **[!UICONTROL OK]** 更新每个用户的权限级别。

   1. 要更改个人的权限级别，请在列表中查找用户以更改权限级别。 更改将自动保存。

   **`Default`**

   1. 要使此仪表板成为您的默认 [!DNL MBI] 帐户，请单击 **[!UICONTROL Make Default]**.

   **`Remove`**

   1. 要删除仪表板，请单击 **[!UICONTROL Delete Dashboard]**.
