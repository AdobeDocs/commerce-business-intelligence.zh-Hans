---
title: 检查更新周期状态
description: 了解如何检查更新周期状态。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 更新周期进度

当您登录 [!DNL MBI] 功能板中，可通过多种方法来检查上次更新周期的状态。 这完全取决于类型 [用户权限](../administrator/user-management/user-management.md) 你有。

## 为何要检查更新周期状态？

当您审计中的数据时，检查状态更新周期很有用 [!DNL MBI] 帐户。 如果您看到 [不符合您期望的结果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)例如，以下位置的每日销售额： [!DNL MBI] 与您在eCommerce平台或 [[!DNL Google] 电子商务收入](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) 您可以检查最后一个数据点，以查看更新完成后问题是否得到解决。

## [!UICONTROL Read-Only] 和 [!UICONTROL Standard]**用户

`Read-only` 用户可以登录其功能板，通过将鼠标悬停在页面右上角的图标上，查看数据更新的最近时间。 这会显示何时提取最后一个数据点。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] 用户

`Admin` 用户可以登录功能板，查看上面的最后一个数据点以及其帐户集成的简短状态图标。

有关更多详细信息，管理员用户可以单击 **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

此页面显示当前更新状态和上次完成更新的时间。

如果更新正在进行，您会看到一个链接，用于在更新完成后请求电子邮件通知。

如果更新未进行，您会看到一个链接，用于强制开始更新。

>[!NOTE]
>
>如果您有中断时间（您不想要的时间） [!DNL MBI] 以更新您的数据)，强制更新会启动一个不遵守这些封锁时间限制的更新周期。
