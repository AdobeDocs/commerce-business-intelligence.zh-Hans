---
title: 更改量度的操作表
description: 了解如何更改量度用于执行其操作的数据表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 更改量度的操作表

在某些情况下，您可以决定更改量度用来执行操作的数据表。 例如，如果您有新的用户表，那么要从以下位置迁移与用户相关的量度：  `Users\_Old` 要使用 `Users\_New` 改为使用表格。

1. 转到 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 单击 **[!UICONTROL Edit]** ，位于您要为其切换 `operational` 表格。
1. 在编辑器中，单击 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. 选择要作为此量度基础的新表。
1. 将现有数据维度与新表中的相应维度匹配。 例如，如果您有一个名为 `User's registration date`，只需选择新表中记录相同日期数据的列。 （如果新表中没有匹配的列，请参阅下一步）

   ![](../../assets/change-metrics-2.png)

1. 如果新表中没有匹配的列，您可以 **在数据表中创建它** 或 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果是由创建的计算列或维度 [!DNL Commerce Intelligence]. 您还可以 **从量度中删除维度**. 要删除您不再需要的维度，只需返回量度的编辑器，然后选择要在其下删除的维度 `Dimensions`.

   ![](../../assets/change-metrics-3.png)
