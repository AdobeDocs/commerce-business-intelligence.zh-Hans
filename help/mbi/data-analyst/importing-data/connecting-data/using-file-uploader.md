---
title: 使用文件上传程序
description: 了解如何将您的所有数据放在一个Data warehouse中。
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# 使用文件上传程序

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] 不仅因为其可视化功能，而且还因为它使您能够将所有数据放在一个Data warehouse中。 甚至位于数据库和集成之外的数据也可以引入 [!DNL Commerce Intelligence] 通过使用Data warehouse管理器中的文件上传工具。

以广告营销活动为例。 如果您同时运行在线和离线营销活动，并且只分析来自在线集成的数据，则无法全面了解营销活动。 通过上传包含离线促销活动数据的电子表格，您可以分析这两组数据，并更深入地了解促销活动效果。

## 限制和要求 {#require}

1. **唯一支持的文件上传格式为 `CSV` 或`comma separated values`**. 如果您使用Excel，则可以使用“另存为”功能将文件保存到 `.csv` 格式。
1. **`CSV`文件必须使用`UTF-8 encoding`**. 大多数情况下，这并不是问题。 如果您在上传文件时遇到此错误， [请参阅此支持文章](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **文件不能大于100MB**. 如果文件大于此值，请将表分成块，并将它们另存为单独的文件。 您可以在加载初始文件后附加数据。
1. **所有表必须具有`primary key`**. 您的表中至少需要有一列可用作 `primary key`，或表中每一行的唯一标识符。 任何指定为 `primary key` 可以 *从不* 为空。 A `primary key` 可以简单到为每一行添加一个提供数字的列，也可以是两个连接在一起的列，以形成一列唯一值(例如， `campaign name` 和 `date`)。

   如果列（或列）被指定为唯一的，但存在重复项，则不会导入重复行。

## 格式化要上载的数据 {#formatting}

将数据上传到之前 [!DNL Commerce Intelligence]，检查它是否根据此部分中的指南进行格式设置。

### 标题行 {#header}

要确保正确标记和导入列，请确保电子表格的第一行是描述每列中数据的标题。

列名必须是唯一的，并且只包含字母、数字、空格和以下符号： `$ % # /`. 如果列名称包含逗号，则在文件上传时将它拆分为两列。 此外，Adobe建议文件中的列数少于85列以优化更新速度。

### 带逗号的数据 {#commas}

因为文件必须位于 `CSV` 格式，使用逗号可能会导致上传数据时出现问题。 `CSV` 文件使用逗号表示新值，因此具有如下名称的列 `Campaigns`， `August` 读为两列(`Campaigns` 和 `August`)而不是1，将所有数据移动一行。 Adobe建议尽可能避免使用逗号。 您可以使用 `Data Preview` 查看更新完成后数据是否正确显示。

### 日期

任何包含日期的数据集都必须使用 [标准日期格式](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` 或 `MM/DD/YYYY`.

### 特殊字符

不接受某些特殊字符。 例如，管道符号 `& # 1 2 4` 将解释为创建列，并在上传文件时导致错误。

### 小数

货币值应具有数据类型 `Decimal Number` 选中，这些列会自动舍入到Data warehouse中的两位小数。 如果不想对小数进行四舍五入或精度大于此值，则应选择 `Non-Currency Decimal Number` 数据类型。

### 百分比

百分比必须以小数形式输入。 例如：

| **右：** | **错误：** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### 前导和/或尾随零的值 {#zeroes}

文件中的某些值（如邮政编码和ID）可能以零开头或结尾。 要确保正确保留和上传零，可以更改格式类型(例如， [从数字到文本](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us))或强制数字格式化。

使用 `US ZIP codes` 有关如何更改数字格式的示例。 In [!DNL Excel]，突出显示包含 `ZIP codes` 和 [更改数字格式](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) 到 `ZIP code`. 您还可以选择自定义数字格式，并在 `Type` 窗口，输入 `00000`. 请记住，如果某些代码的格式为，此方法可能会出现问题 `00000` 而其他 `00000-0000`.

此 `Type` 可以是 [格式不同，以适应其他数据类型](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us)，如ID。 如果 `ID` 长度为九位数，例如 `Type` 可以是 `000000000` 或 `000-000-000`. 这种情况会改变 `123456` 到 `000-123-456`.

对象 [!DNL Google Docs] 和 [!DNL Apple Numbers] 资源，请参阅 [相关](#related) 列表来查看本页底部的URL。

## 上传数据 {#uploading}

现在，您的电子表格已正确格式化， [!DNL Commerce Intelligence]-friendly，将其添加到您的Data warehouse。

1. 要开始配置，请转到 **[!UICONTROL Data** > **File Uploads]**.

1. 单击 **[!UICONTROL Upload to New Table]** 选项卡。

1. 单击 **[!UICONTROL Choose File]** 并选择文件。 单击 **[!UICONTROL Open]** 以开始上传。

   上传完成后，列的列表 [!DNL Commerce Intelligence] “在文件中找到”会显示。

1. 检查列名和数据类型是否正确。 具体而言，检查是否将任何日期列读取为日期，而不是数字。

   >[!NOTE]
   >
   >此 `datatype` 非常重要，因此请勿跳过此步骤！

1. 选择构成列的列 `primary key` 使用键图标下的复选框访问表格。

1. 命名表。

1. 单击 **[!UICONTROL Save Table]**.

A *成功！* 保存表后，屏幕顶部将显示消息。

如果您需要视觉效果，请查看整个过程：

![](../../../assets/fileupload.gif)

上传的表显示在下 **文件上传** “Data warehouse管理器”中表列表的部分（在“所有表”和“同步表”选项中）：

![](../../../assets/upload-tables.png)

## 更新数据或将数据附加到现有表 {#appending}

是否获得了一些要添加到已上传文件的新数据？ 没有问题 — 您可以轻松地更新并附加数据 [!DNL Commerce Intelligence].

1. 要开始配置，请转到 **[!UICONTROL Manage Data** > **File Uploads]**.

1. 单击 **[!UICONTROL Edit/Upload `.csv`到现有表]** 选项卡。

1. 在下拉列表中，单击要更新或附加的表的名称。

1. 使用下拉菜单选择用于处理重复行的选项：

   | Option | 描述 |
   |---|---|
   | `Overwrite old row with new row` | 如果现有表和新文件中某行具有相同的主键，则用新数据覆盖现有数据。 这是用于具有随时间变化的值的列（例如，状态列）的方法。 现有数据将被覆盖并使用新数据更新。 具有不在现有表中的主键的行将作为新行添加。 |
   | `Retain old row; discard new row` | 如果某行在现有表和新文件中具有相同的主键，这会导致忽略新数据。 |
   | `Purge all existing rows first and ignore duplicate keys within the file` | 这将删除任何现有数据，并将其替换为文件中的新数据。 仅当不需要现有表中的任何数据时，才使用此选项。 |

1. 单击 **[!UICONTROL Choose File]** 并选择文件。

1. 单击 **[!UICONTROL Open]** 以开始上传。

   上传完成后， [!DNL Commerce Intelligence] 将验证文件中的数据结构。 A *成功！* 保存表后，屏幕顶部将显示消息。

## 数据可用性 {#availability}

与计算列一样，来自文件上传的数据在下一个更新周期完成后可用。 如果在文件上传期间正在进行更新，则数据将在下次更新后才能使用。 更新周期完成后，您可以导航到 `Data Preview` data warehouse选项卡，以确保文件正确上传且数据按预期显示。

## 总结 {#wrapup}

本主题仅介绍使用导入数据的基础知识，但您可能希望执行一些更高级的操作。 有关格式化和导入金融、电子商务、广告支出和其他类型数据的指导，请参阅相关文章。

此外，文件上传并不是将数据导入 [!DNL Commerce Intelligence]. 此 [数据导入API](https://developer.adobe.com/commerce/services/reporting/import-api/) 函数允许您将任意数据推送到 [!DNL Commerce Intelligence] data warehouse。

## 相关 {#related}

* [格式化和导入财务数据](../../../best-practices/format-import-financial-data.md)
* [导入离线/其他广告支出数据](../connecting-data/import-offline-ad-data.md)
* [预期[!DNL Google ECommerce] 数据](../integrations/google-ecommerce-data.md)

## 第三方资源

* [数字数据格式指南](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] 数据格式指南](https://support.google.com/docs/answer/56470?hl=en)
