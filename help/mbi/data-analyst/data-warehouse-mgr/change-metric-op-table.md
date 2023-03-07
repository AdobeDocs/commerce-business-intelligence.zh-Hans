---
title: 更改量度的操作表
description: 了解如何更改量度用于执行其操作的数据表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 更改量度的操作表

在某些情况下，您可以决定更改量度用来执行操作的数据表。 例如，如果您有一个新的用户表，则要将与用户相关的量度从“Users\_Old”表中迁移出来，改用“Users\_New”表。

1. 转到 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 单击 **[!UICONTROL Edit]** ，位于要切换的指标旁边 `operational` 表格。
1. 在编辑器中，单击 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. 现在，选择要作为此量度基础的新表。
1. 接下来，您必须将现有数据维度与新表中对应的数据维度进行匹配。 例如，如果您有一个名为 `User's registration date`，只需选择新表中的哪一列记录相同的日期数据即可。 （如果新表中没有匹配的列，请参阅下一步）

   ![](../../assets/change-metrics-2.png)

1. 如果新表中没有匹配的列，则可以 **在数据表中创建它** 或 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如果它是计算列或维度，建立者为 [!DNL MBI])。 您还可以 **从量度中删除维度**. 要删除您不再需要的维度，只需返回量度的编辑器，然后选择要删除的维度下 `Dimensions`.

   ![](../../assets/change-metrics-3.png)
