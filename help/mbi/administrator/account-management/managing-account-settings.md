---
title: 管理您的帐户设置
description: 了解如何为Data warehouse自定义帐户设置。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 自定义帐户设置

>[!NOTE]
>
>需要 [管理员权限。](../../administrator/user-management/user-management.md)

在您的 [!DNL MBI] 帐户，您可以为Data warehouse自定义帐户设置。 选择位于任何屏幕右上角的组织名称，然后选择 **[!UICONTROL Account Settings]** 从下拉菜单中查找。

* **[!UICONTROL Client Name:]** 此设置将显示在所有功能板的右上角，以及帐户中的其他位置。 如果您想更改 **[!UICONTROL "Vandelay Industries Co., Ltd]** 转换为 **[!UICONTROL "Vandelay]**，这是执行此操作的位置。

* **[!UICONTROL Currency:]** 这是 *默认货币* 所有货币值。 无论何时将小数或货币值同步到Data warehouse中，此设置都会确定报表中放置在该值之前的符号。

* **[!UICONTROL Blackout Hours:]** 此设置确保在一天中的选定小时内，您的Data warehouse不会访问连接的数据库。 所有小时均以零小时和东部标准时间(EST)表示。 例如，如果您不希望在EST上午9:00到EST下午1:00之间访问生产数据库，则应键入以下数字数组： **9、10、11、12**.

* **[!UICONTROL Forced update hours:]** 此设置可确保自动在您的帐户中开始Data warehouse更新 *在小时内* 您已指定。 与中断时间一样，这些时间也在东部时间中。 例如，如果您希望Data warehouse更新自动从 **午夜** 和 **中午** EST，应键入以下数字数组： **0， 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此选项管理计划发送电子邮件摘要的情况 *在其某个报表中的数据之前* 已刷新。 如果您选择 **否**，则您的帐户会在其计划时间跳过发送电子邮件。 而是在数据更新后由您的帐户发送。 如果您选择 **[!UICONTROL Yes]**，则您的帐户会发送电子邮件，其中包括一则说明数据已过时的消息，并在数据更新后发送另一封电子邮件。

* **[!UICONTROL Enable data updates:]** 此选项可确保数据更新在您的帐户上运行。 如果将设置更改为 **[!UICONTROL No]**，数据同步和列计算在您的帐户中停止。

>[!NOTE]
>
>确保选择 **[!UICONTROL Save Customizations]** 进行更改之后。
