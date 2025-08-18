---
title: 管理您的帐户设置
description: 了解如何自定义Data Warehouse的帐户设置。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 自定义帐户设置

>[!NOTE]
>
>需要[管理员权限。](../../administrator/user-management/user-management.md)

在您的[!DNL Commerce Intelligence]帐户中，您可以自定义Data Warehouse的帐户设置。 可以通过选择位于任何屏幕右上角的组织名称，然后从下拉列表中选择&#x200B;**[!UICONTROL Account Settings]**&#x200B;来访问这些内容。

* **[!UICONTROL Client Name:]**&#x200B;此设置将显示在所有功能板的右上角，以及您帐户内的其他位置。 如果您要将&#x200B;**[!UICONTROL "Vandelay Industries Co., Ltd]**&#x200B;更改为仅&#x200B;**[!UICONTROL "Vandelay]**，则可以在以下位置执行此操作。

* **[!UICONTROL Currency:]**&#x200B;这是您帐户中所有货币值的&#x200B;*默认货币*。 无论何时将小数或货币值同步到Data Warehouse中，此设置都会确定报表中放置在该值之前的符号。

* **[!UICONTROL Blackout Hours:]**&#x200B;此设置可确保在一天中的选定小时内，您的Data Warehouse不会访问连接的数据库。 所有小时均以零小时和东部标准时间(EST)表示。 例如，如果您不希望在EST上午9:00到下午1:00之间的小时访问生产数据库，则应键入以下数字数组： **9、10、11、12**。

* **[!UICONTROL Forced update hours:]**&#x200B;此设置确保在指定的小时内&#x200B;*自动在您的帐户*&#x200B;中开始Data Warehouse更新。 与断电时间一样，这些时间也在东部时间中。 例如，如果您希望Data Warehouse更新在&#x200B;**午夜**&#x200B;和&#x200B;**中午** EST自动开始，则应键入以下数字数组： **0、12**。

* **[!UICONTROL Send email summaries if the data has not updated yet:]**&#x200B;此选项管理计划在其报告&#x200B;*中的数据刷新之前发送*&#x200B;电子邮件摘要的情况。 如果您选择&#x200B;**否**，则您的帐户将在其计划时间跳过发送电子邮件。 而是在数据更新后，由您的帐户发送。 如果选择&#x200B;**[!UICONTROL Yes]**，您的帐户将发送电子邮件，并包含说明数据已过期的消息，并在数据更新后发送另一封电子邮件。

* **[!UICONTROL Enable data updates:]**&#x200B;此选项可确保数据更新在您的帐户上运行。 如果将设置更改为&#x200B;**[!UICONTROL No]**，则帐户中的数据同步和列计算将停止。

>[!NOTE]
>
>确保在进行任何更改后选择&#x200B;**[!UICONTROL Save Customizations]**。
