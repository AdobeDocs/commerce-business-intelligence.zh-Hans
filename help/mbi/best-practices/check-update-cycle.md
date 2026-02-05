---
title: 检查更新周期状态
description: 了解如何检查更新周期状态。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: 776b4b666c47775a7b883a3a6f71c16b4b3bfbad
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 更新周期进度

登录[!DNL Adobe Commerce Intelligence]仪表板时，可通过多种方式检查上次更新周期的状态。 这取决于您拥有的[用户权限](../administrator/user-management/user-management.md)的类型。

## 为何要检查更新周期状态？

当您审核[!DNL Commerce Intelligence]帐户中的数据时，检查状态更新周期很有用。 如果您看到的[个结果不符合您的预期](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)，例如[!DNL Commerce Intelligence]中的每日销售额与您在电子商务平台或[[!DNL Google] 电子商务收入](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html)中看到的结果不匹配，您可以检查最后一个数据点，以查看在更新完成后问题是否得到解决。

## [!UICONTROL Read-Only]和[!UICONTROL Standard]用户

`Read-only`用户可以登录其仪表板，通过将鼠标悬停在页面右上角的图标上，查看数据更新的最近时间。 这会显示何时提取最后一个数据点。

![上次成功的数据更新时间戳显示在接口](../../mbi/assets/last-success-data.png)中

## [!UICONTROL Admin]用户

`Admin`用户可以登录到仪表板并查看上面的最后一个数据点，以及帐户集成的简短状态图标。

有关详细信息，管理员用户可以单击&#x200B;**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**。

![管理数据集成页面，显示连接详细信息和更新状态](../../mbi/assets/detail-manage-data-integrations.png)

此页面显示当前更新状态和上次完成更新的时间。

如果更新正在进行，您会看到一个链接，用于在更新完成后请求电子邮件通知。

如果更新未进行，您会看到一个链接来强制启动更新。

>[!NOTE]
>
>如果您设置了封锁时间（您不希望[!DNL Commerce Intelligence]更新数据的时间），则强制更新会启动一个不遵守封锁时间限制的更新周期。


## 使用API检查更新周期状态

您可以使用&#x200B;**更新周期状态API**&#x200B;检索最近完成的更新周期。

**请求**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**响应（示例）**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

有关参数、身份验证、错误和速率限制，请参阅开发人员文档中的[更新周期状态API](https://developer.adobe.com/commerce/services/reporting/update-cycle/)。
