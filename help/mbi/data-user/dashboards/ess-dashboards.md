---
title: 功能板
description: 了解如何创建和使用功能板。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 功能板

[!DNL MBI] 功能板可让您快速查看商店的绩效和销售活动。 单个功能板可以与其他用户共享，并组织为逻辑组。 您还可以为其他用户设置不同级别的权限。

创建新报表、将其添加到功能板并将数据导出到Excel非常简单。 可以调整图表和报表的大小并将其拖动到功能板上的位置。

![功能板](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 创建功能板 {#createdash}

功能板本质上是可共享的主题存储段，用于您在Report Builder中创建的分析。 这就是您如何鼓励团队在整个组织内进行协作并维护单一的真相来源。

*如果您是管理员或标准用户*，则可以通过单击 `Dashboard Options` 下拉列表和选择 `Create New dashboard`.

您创建的功能板的外观完全由您来决定。 您可以根据需要和工作流程，以任何方式排列和调整功能板中的元素大小。

![调整仪表板大小](../../assets/arrange_resize_dashboard_element.gif)

### 创建新功能板

1. 在菜单中，单击 **[!UICONTROL Dashboards]**.

1. 默认功能板的名称显示在功能板标题的左上角。 单击向下箭头(![](../../assets/magento-bi-btn-down.png))以显示可用选项。

   ![创建功能板](../../assets/magento-bi-dashboard-create.png)

1. 单击 **[!UICONTROL Create Dashboard]**. 然后，执行以下操作：

   * 输入 `Name` 功能板。

   * 创建新 `Group` 在功能板中，输入群组的名称。

      例如，如果Commerce安装有多个商店视图，则可以为每个商店视图创建一个群组。

   * 单击 **[!UICONTROL Create]**.

   ![功能板名称](../../assets/magento-bi-dashboard-create-name.png)

   * 新功能板的名称显示在左上角。 单击向下箭头(![](../../assets/magento-bi-btn-down.png))以显示选项。 如果您创建了群组，则新功能板将显示在列表中该群组的下方。


### 添加报表

1. 要添加报表，请执行以下操作之一：

   * 单击 **[!UICONTROL Add a report]** 提示。

   * 在功能板标题中，单击 **[!UICONTROL Add Report]**.

      ![添加报表](../../assets/magento-bi-dashboard-create-add-report.png)

1. 单击 **[!UICONTROL Create Report]** 显示 **[!UICONTROL Report Builder Options]**.

   ![Report Builder选项](../../assets/magento-bi-report-builder.png)

## 在功能板上排列项目

* 要调整图表或报表的大小，请将右下角拖动到新大小。

* 要移动图表或报表，请将鼠标悬停在标题或标题上，直到光标变为十字。 然后，将其拖动到位置。

## 管理功能板 {#managedash}

在 **[!DNL Manage Data** > **Dashboards]**，您可以管理您拥有的功能板的用户权限，删除不再需要的功能板，并设置默认功能板。

### 共享功能板 {#sharingdash}

真正扩展 [!DNL MBI] 在整个组织中，我们鼓励您与其他团队成员共享您创建的功能板，并提供有价值的分析。 *您可以共享您拥有的功能板* 单击 `Share Dashboard` 选项。

当您共享功能板时，您可以在组织内或在单个基础上分配权限，这意味着您可以决定谁可以查看和编辑您的报表。

>[!NOTE]
>
>`Read-Only` 用户只能访问直接与他们共享的功能板 — 他们无法自行搜索和添加功能板。 不要忘记让他们陷入循环！

### 访问共享功能板 {#accessshared}

*如果您是管理员或标准用户* 并想要将共享功能板添加到您的帐户，您可以通过单击 **[!UICONTROL Dashboard Options]** 然后单击 **[!UICONTROL Find]** 中。

![查找功能板](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 管理功能板设置

1. 在菜单中，单击 **[!DNL Manage Data** > **Dashboards]**.

1. 如果适用，请输入新 `Dashboard Name`.

1. 将功能板分配给 `Dashboard Group`，从组列表中进行选择。

   **`Permissions`**

   要向所有用户授予对功能板的相同级别访问权限，请执行以下操作：

   1. 在 **`Shared with`**，选择以下选项之一：

      * `View`
      * `Edit`
      * `None`
   1. 提示确认时，单击 **[!UICONTROL OK]** 更新每个用户的权限级别。

   1. 要更改个人的权限级别，请在列表中找到用户更改权限级别。 更改将自动保存。

   **`Default`**

   1. 要将此功能板设为 [!DNL MBI] 帐户，单击 **[!UICONTROL Make Default]**.

   **`Remove`**

   1. 要删除功能板，请单击 **[!UICONTROL Delete Dashboard]**.
