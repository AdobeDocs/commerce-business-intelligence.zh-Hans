---
title: 连接Adobe Analytics
description: 了解如何集中对的端到端客户历程的关注 [!DNL Adobe Analytics] 而电子商务正是您赖以生存的 [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

此 [!DNL Adobe Analytics] 集成 [!DNL Adobe Commerce Intelligence] 使您能够集中对端到端客户历程的关注 [!DNL Adobe Analytics] 而电子商务正是您赖以生存的 [!DNL Commerce Intelligence]. 这可让您全面了解商店的整体性能。

更具体地说， [!DNL Adobe Analytics] 集成 [!DNL Commerce Intelligence] 为商家提供开始组合其 [!DNL Adobe Commerce] 和 [!DNL Adobe Analytics] 数据集。

- 从现有资源创建连接 [!DNL Adobe Analytics] 帐户至 [!DNL Commerce Intelligence].

- 从一个报表包中选择最多25个量度和维度以复制到您的Data warehouse中。

- 使用所有标准 [!DNL Commerce Intelligence] 用于转换、加入和报告复制数据的功能 [!DNL Adobe Analytics] 数据。

## 连接先决条件

连接时需要以下信息：

- [!DNL Adobe Analytics] 登录凭据

- `Name` 和/或 `ID` 之 [!DNL Adobe Analytics] 要从中复制数据的报表包

- 要复制到的量度和维度列表 [!DNL Commerce Intelligence]

## 连接 [!DNL Adobe Analytics] 集成 [!DNL Commerce Intelligence]

1. 转到 `Integrations` 页面位于 **[!DNL Manage Data** > **Integrations]**.

1. 单击 **[!UICONTROL Add an Integration]**.

1. 单击 **[!UICONTROL Adobe Analytics]** 图标以访问允许您授权 [!DNL Adobe Analytics] 帐户连接。

1. 单击 **[!UICONTROL Authorize with Adobe Analytics]**.

1. 输入您的 [!DNL Adobe Analytics] 凭据。 成功授权后，您将被重定向回 [!DNL Commerce Intelligence].

1. 此时将显示可用报表包的列表。 选择要从中导入数据的报表包，然后单击 **[!UICONTROL Continue]**.

1. 此时将显示量度和维度选择屏幕。 选择至少一个量度和至少一个维度，最多总计25个量度和维度。 按名称搜索或滚动以查找组件，然后单击要选择的复选框。 单击 **[!UICONTROL Continue]**.

1. 选定的报表包会显示在表格中。 单击 **[!UICONTROL Save]** 以确认您的选择。

1. 通知 [!DNL Commerce Intelligence] [支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 您的集成已获得授权，并且他们会为您运行初始连接过程。

运行初始连接进程后，您的表将位于“Data warehouse”页中的 `All Tables` 选项卡。 选择要复制的列，数据将在下次完全更新后显示。
