---
title: 更改量度的操作表
description: 了解如何更改量度用于执行其操作的数据表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 0%

---

# 更改量度的操作表

在某些情况下，您可以决定更改量度用来执行操作的数据表。 例如，如果您有一个新的用户表，您希望从`Users\_Old`表中迁移与用户相关的量度以改用`Users\_New`表。

1. 转到&#x200B;**[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 单击要切换&#x200B;**[!UICONTROL Edit]**&#x200B;表的量度旁边的`operational`。
1. 在编辑器中，单击&#x200B;**[!UICONTROL Change]**。

   ![指标定义页显示操作表设置](../../assets/change-metrics-1.png)
1. 选择要作为此量度基础的新表。
1. 将现有数据维度与新表中的相应维度匹配。 例如，如果您有一个名为`User's registration date`的列，只需选择新表中的哪一列记录相同的日期数据即可。 （如果新表中没有匹配的列，请参阅下一步）

   ![显示可用表的表选择下拉列表](../../assets/change-metrics-2.png)

1. 如果新表中没有匹配的列，您可以&#x200B;**在数据表中创建它**，或者[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)（如果它是由[!DNL Commerce Intelligence]创建的计算列或维度）。 您也可以&#x200B;**从指标**&#x200B;中删除维度。 要删除您不再需要的维度，只需返回量度的编辑器，并在`Dimensions`下选择要删除的维度。

   ![操作列选择下拉菜单](../../assets/change-metrics-3.png)
