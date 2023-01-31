---
title: 导出原始数据
description: 了解如何从 [!DNL MBI] data warehouse，以详细了解功能板的动力。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 导出原始数据

使用原始数据导出，您可以从 [!DNL MBI] data warehouse，以详细了解功能板的动力。 此外，原始数据导出还可以帮助您 [精确数据差异](https://support.magento.com/hc/en-us/articles/360016730631).

原始数据导出允许访问通过取消相关量度的标准化和预聚合生成的其他列和维度。 例如， `User's first order date` 是一个维度，您可以为 [!DNL MBI]，但它可能在数据库中不可用。

本教程涵盖以下内容：

* [选择要导出的数据](#select)
* [下载导出(](#download)
* [访问历史导出](#historical)

## 步骤1:选择要导出的数据 {#select}

在中，可以通过两种方式导出原始数据 [!DNL MBI]:在图表级别或表级别。

### 在 `Manage Data` 选项卡

如果要从中导出表 `Manage Data` 选项卡，您需要 [管理员](../administrator/user-management/user-management.md) 权限。

1. 单击 **[!UICONTROL Manage Data** > **&#x200B;导出数据&#x200B;**> **原始数据导出]** 以开始使用。
1. 您将看到 `Export List` （如果存在）。 单击 **[!UICONTROL Add Export]** 创建新导出。
1. 的 `New Raw Data Export` 对话框。 在此，您可以通过选择或取消选择列和过滤器来自定义导出：

   * `Table` - `Table` 字段选择要从中导出数据的表。 默认情况下，这将显示您导航到的表。
   * `Export Name`  — 在此字段中，输入导出的名称。 例如： `Philadelphia - Daily Revenue`.
   * `Available Columns`  — 此字段列出了数据库中可包含在导出中的列（维度）。 要添加列，请单击其名称。
   * `Selected Columns`  — 此字段列出当前包含在导出中的列（维度）。 要删除列，请单击其名称。
   * `Filter`  — 此部分列出了当前应用于导出的过滤器。 这些过滤器可以更改；还可以添加新过滤器以导出特定数据集。
   * 完成后，单击 **[!UICONTROL Export Data]**.

### 从功能板在图表级别导出

1. 单击任意图表右上角的齿轮图标。
1. 选择 `Raw Export` 从下拉菜单中显示 `Raw Export` 对话框。
1. 通过选择 `table`, `columns`和 `filters` ，以包含或排除。 有关此模块中字段的更多详细信息，请参阅上一节。
   >[!NOTE]
   >
   >在 `Table` 字段，默认为为图表提供支持的表。

1. 完成后，单击 **[!UICONTROL Export Data]**.

让我们在图表级别查看整个过程。

![](../assets/Chart-level_export.gif)

## 步骤2:下载导出 {#download}

完成在 `Raw Data Export` 对话框。 由于某些导出的大小可能较大，因此限制为1000万行，可能需要一些时间才能运行。

要检查导出是否准备就绪，请单击 **[!UICONTROL Raw Data Exports]** 中。 单击 **[!UICONTROL Download]** 下载zip文件 `.csv` 文件。

![](../assets/Downloading_export.gif)

## 步骤3:访问历史导出 {#historical}

要查看以往的导出，请单击 **[!UICONTROL Raw Data Export]** 中。 最长可访问7天的待决和已完成报告。

恭喜！ 你完成了。
