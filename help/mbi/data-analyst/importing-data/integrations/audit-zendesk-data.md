---
title: 审核Zendesk数据
description: 了解导出Zendesk数据的步骤。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# 审核Zendesk数据

在您的[[!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)中发现一些奇怪的内容？ 要查明问题，您需要浏览数据。 可以通过将[!DNL Zendesk]数据导出到可下载的文件来完成此操作。

## 启用数据导出

当前未为所有[!DNL Zendesk]帐户启用数据导出。 要激活此功能，请[提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)，并提及您的[!DNL Zendesk]子域名。

>[!NOTE]
>
>当前只有`Enterprise`和`Plus`计划有权访问此功能。

启用数据导出后，只有特定电子邮件域中的管理员才能从[!DNL Zendesk]帐户导出数据。 此电子邮件域通常是与[!DNL Zendesk]相同的电子邮件域。 默认使用帐户所有者的电子邮件域，但您可以根据需要更改该域。

## 导出到可下载的文件

1. 单击侧边栏中的管理员图标（齿轮徽标），然后选择&#x200B;**[!UICONTROL Manage** > **Reports]**。
1. 单击&#x200B;**[!UICONTROL Export]**&#x200B;选项卡。
1. 单击“Full XML Export（完整XML导出）”旁边的&#x200B;**[!UICONTROL Request file]**，如下图所示。

   此时，将开始生成；完成后，您将通过电子邮件收到通知。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 单击电子邮件通知中的链接以下载包含报表的zip文件。

   此下载链接的有效期至少为3天。

此过程将生成一个XML文件，其中包含存储在当前[!DNL Zendesk]帐户中的所有信息，包括票证数据（包含注释）、用户数据和帐户数据。 此时，您可以[提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)（请确保附加此文件！），以便更仔细地查看您的数据。 如果文件太大，请通过[!DNL Commerce Intelligence]或[!DNL Dropbox]与[!DNL Google Drive]团队共享。

有关[!DNL Zendesk]文件导出的详细信息，请参阅官方的[[!DNL Zendesk] 导出文档](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file)。
