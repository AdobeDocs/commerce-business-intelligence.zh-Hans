---
title: 数据迁移服务
description: 了解提交请求并开始迁移所需的一切。
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 数据迁移

迁移到新的数据库模式、服务器或报告数据库并不一定有压力。 [[!DNL Adobe] 服务团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)提供迁移帮助。

为确保过渡尽可能顺利，提交迁移请求时应尽可能详细。 本主题包含提交请求并开始迁移所需的一切。 向我们提供您需求的全面信息，可以确保您的项目范围设定得当，并且估算准确。

## 快速入门 {#started}

在开始之前，您必须知道以下问题的答案：

* **新数据库是否位于新服务器上？**&#x200B;在提交请求之前，请在&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;下更新数据连接的设置。 如果需要有关如何执行此操作的更新程序，请转到[`Integrations`](../integrations/integrations.md)部分并查找有关您正在使用的数据库类型的说明。

* **您的所有历史数据是否都存在于新数据库中，还是需要迁移？**&#x200B;您可以在迁移过程中合并历史数据和新数据。 即使您不需要整合，也可以在您的请求中告知我们。

获得上述答案后，您需要知道迁移的类型。 新数据库是具有[`same`](#sameschema)架构，还是具有[`different`](#newschema)架构？ 在下面的讨论中，您可以找到每种迁移类型的详细说明。

## 迁移到具有相同模式的新数据库 {#sameschema}

在提交请求时，告诉我们数据库架构没有更改，并且已在[!DNL Adobe Commerce Intelligence]中设置连接。

如果数据库有新名称，请将其包含在请求中，以便您的功能板可以正确迁移。

如果数据库名称未更改，则迁移已完成。 在下次完全更新完成后，功能板和报表将进行刷新。

## 迁移到具有不同模式的新数据库 {#newschema}

>[!IMPORTANT]
>
>如果某些数据列在新数据库中没有等效的列，则可能会在此过程中丢失某些分析。

要成功完成此类型的迁移，现有数据列必须与新数据库中的相应数据列匹配。 这不是强制性的，但是为我们执行匹配有助于加快请求的周转时间并降低迁移成本。

如果您觉得可以自行进行匹配，请按照以下说明将完成的电子表格附加到您的请求：

1. 查看当前同步到Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**)的所有表和列。

1. 在电子表格中，为要迁移到新数据库的每个表创建一个选项卡。

1. 在每个选项卡中，为需要迁移的所有现有列创建一个列。 Adobe建议将其命名为类似`Existing column name`的名称。

1. 您还需要在电子表格的每个选项卡中为新数据库中的列对等项设置另一列。 Adobe建议将该列命名为类似`New column name`的名称。

1. 输入现有列及其等效列。 如果现有列没有新的等效项，请输入`N/A`。

   此外，如果有新方法可计算新数据库中的相同信息，请在[`New column name`]列中输入该信息。

以下是一个示例：

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>如果某些数据列在新数据库中没有等效的列，则可能会在此过程中丢失某些分析。

## 如何提交请求？ {#submitreq}

您可以通过[提交支持请求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)联系我们。

如果您按照上一节中的步骤创建列匹配电子表格，请不要忘记附加它。

## 接下来呢？ {#wrapup}

确定项目的范围需要您与执行迁移的Commerce服务团队的分析人员之间进行一些协作。 更改的复杂性以及您和分析人员的响应能力直接影响迁移所需的时间。 确定详细信息后，将建立时间线并发送工作说明给您。
