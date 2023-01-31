---
title: 检查更新周期状态
description: 了解如何检查更新周期状态。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 更新周期进度

当您登录 [!DNL MBI] 功能板中，有多种方法可检查上次更新周期的状态。 这取决于 [用户权限](../administrator/user-management/user-management.md) 你有。

## 为什么我应检查更新周期状态？

在审核 [!DNL MBI] 帐户。 如果您看到 [不符合预期的结果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)，例如 [!DNL MBI] 与您在电子商务平台或 [[!DNL Google] 电子商务收入](https://support.magento.com/hc/en-us/articles/360016505232) 您可以检查最后一个数据点，以查看更新完成后是否将解决该问题。

## [!UICONTROL Read-Only] 和 [!UICONTROL Standard]**用户

`Read-only` 用户可以登录其功能板，并通过将鼠标悬停在页面右上方的图标上来查看数据的更新日期。 这将显示拉取最后一个数据点的时间。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 用户

`Admin` 用户可以登录功能板并查看上面的最后一个数据点，以及其帐户集成的简短状态图标。

有关更多详细信息，管理员用户可以单击 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

此页面将显示当前更新状态和上次完成更新的时间。

如果当前正在进行更新，您将在更新完成后看到一个链接以请求电子邮件通知。

如果更新未进行，您会看到一个链接以强制启动更新。

>[!NOTE]
>
>如果您有封锁时间(您不希望 [!DNL MBI] 更新数据)集，则强制更新将启动不遵守这些封锁时间限制的更新周期。
