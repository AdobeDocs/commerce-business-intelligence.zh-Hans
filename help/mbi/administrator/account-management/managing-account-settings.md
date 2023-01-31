---
title: 管理帐户设置
description: 了解如何为您的data warehouse自定义大量帐户设置。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 自定义帐户设置

>[!NOTE]
>
>需要 [管理员权限。](../../administrator/user-management/user-management.md)

在 [!DNL MBI] 帐户，则可以为您的data warehouse自定义多个帐户设置。 通过选择任意屏幕右上角的组织名称，然后选择 **[!UICONTROL Account Settings]** 从下拉菜单中。

* **[!UICONTROL Client Name:]** 此设置显示在所有功能板的右上角以及您帐户中的其他位置。 如果您想更改 **[!UICONTROL "Vandelay Industries Co., Ltd]** 仅 **[!UICONTROL "Vandelay]**，这是执行此操作的位置。

* **[!UICONTROL Currency:]** 这是 *默认货币* 帐户中的所有货币值。 无论何时将小数值或货币值同步到您的data warehouse中，此设置都会确定在报表中放置在该值之前的符号。

* **[!UICONTROL Blackout Hours:]** 此设置可确保在一天的选定时间内，您的data warehouse不会访问您连接的数据库。 所有小时都以零小时和东部标准时间(EST)表示。 例如，如果您不希望在东部标准时间上午9:00到下午1:00之间访问生产数据库，则应键入以下数组： **9、10、11、12**.

* **[!UICONTROL Forced update hours:]** 此设置可确保data warehouse更新在您的帐户中自动开始 *小时* 您已指定。 与封锁时间一样，这些时间也在ET中。 例如，如果您希望data warehouse更新自动从 **午夜** 和 **中午** EST，您应键入以下数组： **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此选项用于告知系统在计划发送电子邮件摘要的情况下应执行的操作 *数据之前* 已刷新至当前状态。 如果您选择 **否**，则您的帐户将跳过在计划时间发送电子邮件的过程，而是在数据更新后发送。 如果您选择 **[!UICONTROL Yes]**，则您的帐户将发送电子邮件，并包含一条消息以说明数据已过时，并在数据更新后再发送电子邮件。

* **[!UICONTROL Enable data updates:]** 此选项可确保数据更新在您的帐户上运行。 如果将设置更改为 **[!UICONTROL No]**、数据同步和列计算将完全停止您的帐户。

>[!NOTE]
>
>确保选择 **[!UICONTROL Save Customizations]** 进行任何更改后。
