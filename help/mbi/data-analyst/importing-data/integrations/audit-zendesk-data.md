---
title: 审核Zendesk数据
description: 了解导出Zendesk数据的步骤。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 审核Zendesk数据

在你的身体里发现了一些奇怪的东西 [[!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)？ 要查明问题，您需要浏览数据。 这可以通过导出您的 [!DNL Zendesk] 数据下载到可下载的文件。

## 启用数据导出

当前未对全部启用数据导出 [!DNL Zendesk] 帐户。 要激活此功能， [提交支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)，提及您的 [!DNL Zendesk] 子域名。

>[!NOTE]
>
>仅 `Enterprise` 和 `Plus` 计划当前有权访问此功能。

启用“数据导出”后，只有特定电子邮件域中的管理员才能从 [!DNL Zendesk] 帐户。 此电子邮件域通常与您的电子邮件域相同。 [!DNL Zendesk]. 默认使用帐户所有者的电子邮件域，但您可以根据需要更改该域。

## 导出到可下载的文件

1. 单击侧栏中的管理员图标（齿轮徽标），然后选择 **[!UICONTROL Manage** > **Reports]**.
1. 单击 **[!UICONTROL Export]** 选项卡。
1. 单击 **[!UICONTROL Request file]** “完整XML导出”旁边，如下图所示。

   此时，将开始生成；完成生成后，您将通过电子邮件收到通知。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 单击电子邮件通知中的链接以下载包含报表的zip文件。

   此下载链接的有效期至少为3天。

此过程会生成一个XML文件，其中包含当前存储的所有信息 [!DNL Zendesk] 帐户，包括票证数据（含注释）、用户数据和帐户数据。 此时，您可以 [提交支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （请务必附加此文件！） 以便更仔细地查看您的数据。 如果文件太大，请将其与 [!DNL Commerce Intelligence] 团队： [!DNL Dropbox] 或 [!DNL Google Drive].

有关详情，请参阅 [!DNL Zendesk] 文件导出，请参阅 [[!DNL Zendesk] 导出文档](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
