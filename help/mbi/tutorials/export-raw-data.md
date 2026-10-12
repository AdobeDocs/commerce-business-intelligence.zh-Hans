---
title: 导出原始数据
description: 了解如何从[!DNL Commerce Intelligence] Data Warehouse导出记录，以进一步了解为您的仪表板提供支持的功能。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Developer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
TQID: 'https://experienceleague.adobe.com/8n0DUwkiI1BVF5612vCd4jFWx7jwWlfOHg2K3hgWkco'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%
---
# 导出原始数据

使用原始数据导出，您可以从Data Warehouse导出记录，以更详细地了解为您的仪表板提供支持的功能。 此外，原始数据导出还可以帮助您[查明数据差异](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies)。

通过原始数据导出，可访问通过取消标准化和预聚合相关量度生成的其他列和维度。 例如，`User's first order date`是一个维度，您可以为[!DNL Commerce Intelligence]中的每个用户导出该维度，但它可能在数据库中不可用。

本教程涵盖以下内容：

* [选择要导出的数据](#select)
* [正在下载导出（`.csv`文件）](#download)
* [访问历史导出](#historical)

## 步骤1：选择要导出的数据 {#select}

有两种方式可以在[!DNL Commerce Intelligence]中导出原始数据：

1. 在图表级别
1. 在表级别

### 在[!UICONTROL Manage Data]选项卡的表级别导出

如果要从[!UICONTROL Manage Data]选项卡导出表，则需要[管理员](../administrator/user-management/user-management.md)权限。

1. 单击&#x200B;**[!UICONTROL Manage Data** > **&#x200B;导出数据&#x200B;**> **原始数据导出]**。
1. 您会看到`Export List`个最近创建的数据导出（如果存在）。 单击&#x200B;**[!UICONTROL Add Export]**&#x200B;以创建导出。
1. 将显示`New Raw Data Export`对话框。 在此，您可以通过选择或取消选择列和筛选器来自定义导出：

   * `Table` - `Table`字段选择从中导出数据的表。 默认情况下，这会显示您导航到的表。
   * `Export Name` — 在此字段中，输入导出的名称。 例如： `Philadelphia - Daily Revenue`。
   * `Available Columns` — 此字段列出数据库中可包含在导出中的列（维度）。 要添加列，请单击其名称。
   * `Selected Columns` — 此字段列出当前包含在导出中的列（维度）。 要删除列，请单击其名称。
   * `Filter` — 此部分列出当前应用于导出的筛选器。 这些筛选器可以更改；还可以添加新的筛选器以导出特定数据集。
   * 完成后，单击&#x200B;**[!UICONTROL Export Data]**。

### 从功能板在图表级别导出

1. 单击任何图表右上角的齿轮图标。

1. 从下拉列表中选择`Raw Export`以显示`Raw Export`对话框。

1. 通过选择要包含或排除的`table`、`columns`和`filters`自定义导出。 有关本模块中字段的更多详细信息，请参阅上一节。

   >[!NOTE]
   >
   >默认情况下，`Table`字段中显示的表是为该图表提供支持的表。

1. 完成后，单击&#x200B;**[!UICONTROL Export Data]**。

在图表级别查看整个过程。

![从图表导出原始数据的动画演示](../assets/Chart-level_export.gif)

## 步骤2：下载导出 {#download}

在`Raw Data Export`对话框中完成选择后，将立即开始处理导出。 由于某些导出可能规模较大，因此限制为1000万行，并且运行可能需要一些时间。

要检查导出是否已准备就绪，请单击屏幕右上角的&#x200B;**[!UICONTROL Raw Data Exports]**。 单击&#x200B;**[!UICONTROL Download]**&#x200B;可下载导出的压缩`.csv`文件。

![下载导出的CSV文件的动画演示](../assets/Downloading_export.gif)

## 步骤3：访问历史导出 {#historical}

要查看您过去的导出，请单击屏幕右上角的&#x200B;**[!UICONTROL Raw Data Export]**。 待定和已完成报告最多可存取7天。
