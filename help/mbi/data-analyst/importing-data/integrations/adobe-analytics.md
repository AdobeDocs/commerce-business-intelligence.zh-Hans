---
title: Connect Adobe Analytics
description: 了解如何将 [!DNL Adobe Analytics] 以及您所依赖的电子商务焦点 [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 连接 [!DNL Adobe Analytics]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

的 [!DNL Adobe Analytics] 集成 [!DNL MBI] 使您能够将 [!DNL Adobe Analytics] 以及您所依赖的电子商务焦点 [!DNL MBI]，以更全面地了解您商店的整体性能。

更具体地说， [!DNL Adobe Analytics] 集成 [!DNL MBI] 为商户提供了开始组合其商务和Analytics数据集的功能。
- 从现有的 [!DNL Adobe Analytics] 帐户 [!DNL MBI].
- 从一个报表包中选择最多25个要复制到 [!DNL MBI] data warehouse。
- 使用所有标准 [!DNL MBI] 转换、连接和报告已复制内容的功能 [!DNL Adobe Analytics] 数据。

## 连接先决条件

连接时需要以下信息：
- [!DNL Adobe Analytics] 登录凭据
- `Name` 和/或 `ID` of [!DNL Adobe Analytics] 报表包从
- 要复制到 [!DNL MBI]

## 连接 [!DNL Adobe Analytics] MBI集成

1. 转到 `Integrations` 页面下 **[!DNL Manage Data** > **Integrations]**.
1. 单击 **[!UICONTROL Add an Integration]**，位于屏幕右侧。
1. 单击 **[!UICONTROL Adobe Analytics]** 图标以访问允许您 [!DNL Adobe Analytics] 帐户连接。
1. 单击 **[!UICONTROL Authorize with Adobe Analytics]**.
1. 输入 [!DNL Adobe Analytics] 凭据。 成功授权后，您将被重定向回 [!DNL MBI].
1. 此时会显示可用报表包的列表。 选择要从中导入数据的报表包，然后单击 **[!UICONTROL Continue]**.
1. 此时会显示量度和维度选择屏幕。 至少选择一个量度和至少一个维度，最多共25个量度和维度。 按名称搜索或滚动以查找您的组件，然后单击要选择的复选框。 单击 **[!UICONTROL Continue]**.
1. 选定的报表包将显示在表格中。 单击 **[!UICONTROL Save]** 以确认您的选择。
1. 通知 [!DNL MBI] 支持团队已授权您的集成，他们将为您运行初始连接流程。

运行初始连接过程后，您的表将显示在Data warehouse页面的 `All Tables` 选项卡。 选择要复制的列，数据将在下一次完全更新后显示。
