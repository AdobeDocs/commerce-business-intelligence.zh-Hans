---
title: 连接Adobe Analytics
description: 了解如何将 [!DNL Adobe Analytics] 的端到端客户历程重点与您依赖的 [!DNL Commerce Intelligence]的电子商务重点结合起来。
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 连接[!DNL Adobe Analytics]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![](../../../assets/adobe-analytic-slogo.png)

[!DNL Adobe Analytics]的[!DNL Adobe Commerce Intelligence]集成使您能够将[!DNL Adobe Analytics]的端到端客户历程重点与您从[!DNL Commerce Intelligence]依赖的电子商务重点结合起来。 这可让您全面了解商店的整体性能。

更具体地说，[!DNL Adobe Analytics]的[!DNL Commerce Intelligence]集成为商家提供了开始组合其[!DNL Adobe Commerce]和[!DNL Adobe Analytics]数据集的功能。

- 创建从现有[!DNL Adobe Analytics]帐户到[!DNL Commerce Intelligence]的连接。

- 从一个报表包中选择最多25个指标和维度以复制到Data Warehouse中。

- 使用所有标准[!DNL Commerce Intelligence]功能转换、连接和报告复制的[!DNL Adobe Analytics]数据。

## 连接先决条件

连接需要以下信息：

- [!DNL Adobe Analytics]登录凭据

- 要从中复制数据的`Name`和/或`ID`（共[!DNL Adobe Analytics]个报表包）

- 要复制到[!DNL Commerce Intelligence]中的指标和维度列表

## 正在连接[!DNL Adobe Analytics]的[!DNL Commerce Intelligence]集成

1. 转到`Integrations`下的&#x200B;**[!DNL Manage Data** > **Integrations]**&#x200B;页面。

1. 单击&#x200B;**[!UICONTROL Add an Integration]**。

1. 单击&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;图标可访问允许您授权您的[!DNL Adobe Analytics]帐户连接的页面。

1. 单击&#x200B;**[!UICONTROL Authorize with Adobe Analytics]**。

1. 输入您的[!DNL Adobe Analytics]凭据。 成功授权后，您将被重定向回[!DNL Commerce Intelligence]。

1. 此时将显示可用报表包的列表。 选择要从中导入数据的报表包，然后单击&#x200B;**[!UICONTROL Continue]**。

1. 此时将显示量度和维度选择屏幕。 选择至少一个量度和至少一个维度，最多总共25个量度和维度。 按名称搜索或滚动以查找组件，然后单击复选框以选择。 单击&#x200B;**[!UICONTROL Continue]**。

1. 选定的报表包会显示在表格中。 单击&#x200B;**[!UICONTROL Save]**&#x200B;确认您的选择。

1. 通知[!DNL Commerce Intelligence] [支持团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)您的集成已获得授权，他们将为您运行初始连接进程。

运行初始连接进程后，您的表将在Data Warehouse页面的`All Tables`选项卡下可用。 选择要复制的列，数据将在下次完全更新后显示。
