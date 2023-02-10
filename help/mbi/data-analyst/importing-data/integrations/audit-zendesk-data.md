---
title: 审核Zendesk数据
description: 了解导出Zendesk数据的步骤。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 审核Zendesk数据

在你的 [[!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)? 为了查明问题，我们需要探索您的数据。 这可以通过导出 [!DNL Zendesk] 数据到可下载文件。

## 启用数据导出

当前并未为所有人启用数据导出 [!DNL Zendesk] 帐户。 要激活此功能，请 [提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en)，提及 [!DNL Zendesk] 子域名。

>[!NOTE]
>
>仅 `Enterprise` 和 `Plus` 计划当前有权访问此功能。

启用数据导出后，只有特定电子邮件域中的管理员才能从 [!DNL Zendesk] 帐户。 此电子邮件域通常与 [!DNL Zendesk]. 默认使用帐户所有者的电子邮件域，但您可以根据需要更改该域。

## 导出到可下载的文件

1. 单击侧栏中的管理员图标（齿轮徽标），然后选择 **[!UICONTROL Manage** > **Reports]**.
1. 单击 **[!UICONTROL Export]** 选项卡。
1. 单击 **[!UICONTROL Request file]** ，如下图所示。

   此时，将开始构建；完成时，将通过电子邮件通知您。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. 单击电子邮件通知中的链接以下载包含报表的zip文件。

   此下载链接至少有三天有效。

此过程会生成一个XML文件，其中包含当前存储在您当前 [!DNL Zendesk] 帐户，包括票证数据（含注释）、用户数据和帐户数据。 此时，您可以 [提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) （请务必附加此文件！） 以便我们更仔细地查看您的数据。 如果文件过大，请将其与 [!DNL MBI] 团队通过 [!DNL Dropbox] 或 [!DNL Google Drive].

有关 [!DNL Zendesk] 文件导出，请参阅 [[!DNL Zendesk] 导出文档](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
