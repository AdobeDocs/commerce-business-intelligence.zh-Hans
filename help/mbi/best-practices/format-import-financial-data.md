---
title: 格式化并导入财务数据
description: 了解如何格式化并导入财务数据。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 格式化和导入财务数据

本主题将讨论导入财务数据以便在中分析的最佳方法 [!DNL Adobe Commerce Intelligence].

二维交叉表数据表通常是用于财务数据的格式。 由于列和行中的值均按标签进行分类，因此这种类型的布局可能很容易通过人眼和电子表格工具查看，但对数据库并不友好。

![](../../mbi/assets/crosstab.png)

要在中导入和分析此数据，请执行以下操作 [!DNL Commerce Intelligence]，则表必须拼合到一维列表中。 拼合时，每个数据值都按多个标签进行分类，这些标签全部位于一行中，其中每一行都是唯一的，或者具有唯一的标识符，例如主键列。

![](../../mbi/assets/flattened.png)

## 设置导入的Excel文件格式

使用平面化二维表 [!DNL Excel] 数据透视表：

1. 使用二维数据表打开文件。
1. 打开数据透视表向导。 在 [!DNL Windows]，快捷键为 `Alt-D`. 在 [!DNL Mac OS]，输入 `Command-Option-P`.
1. 选择 **[!UICONTROL Multiple consolidated ranges]** 并单击 **[!UICONTROL Next]**.
1. 选择 **[!UICONTROL I will create the page fields]** 并单击 **[!UICONTROL Next]**.
1. 在二维表中选择整个数据集，包括标签。 确保 `0` 选定作为所需页面字段数，然后单击 **[!UICONTROL Next]**.
1. 在新工作表中创建数据透视表并单击 **[!UICONTROL Finish]**.
1. 从字段列表中取消选择列和行字段。
1. 双击生成的数值可在新工作表中显示展平的源数据。
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 另存为 `CSV` 文件。

## 正在结束

数据表已转换为列表格式，并保留其所有原始信息，现在可以 [导入到 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 以供分析。
