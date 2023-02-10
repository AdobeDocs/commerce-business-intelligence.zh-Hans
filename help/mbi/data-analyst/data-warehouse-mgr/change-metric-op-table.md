---
title: 更改量度的操作表
description: 了解如何更改量度用于执行其操作的数据表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 更改量度的操作表

在某些情况下，您可能会决定更改量度用来执行操作的数据表。 例如，如果您有一个新用户表，则需要从“Users\_Old”表迁移与用户相关的量度，以改用“Users\_New”表。

1. 转到 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 单击 **[!UICONTROL Edit]** 的 `operational` 表。
1. 在编辑器中，单击 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. 现在，选择要基于此量度的新表。
1. 接下来，您必须将现有数据维度与新表格中的相应数据维度进行匹配。 例如，如果您有一个名为 `User's registration date`，只需选择新表中记录相同日期数据的列即可。 （如果新表中没有匹配的列，请参阅下一步）

   ![](../../assets/change-metrics-2.png)

1. 如果新表中没有匹配列，则可以 **在数据表中创建它** 或 [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如果它是由 [!DNL MBI])，或者只是 **从量度中删除维度**. 要删除不再需要的维度，只需返回到量度的编辑器，并选择要删除的维度 `Dimensions`.

   ![](../../assets/change-metrics-3.png)
