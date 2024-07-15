---
title: 创建自动化电子邮件摘要
description: 了解如何创建自动化电子邮件摘要。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 创建自动化电子邮件摘要

电子邮件摘要是一种功能强大的通信工具，可用于与关键利益相关者分享您的业务状态和趋势。 借助电子邮件摘要，您可以：

* 通过电子邮件发送包含报告的图形摘要
* 在接收电子邮件时包括或排除电子邮件摘要作者
* 发送电子邮件的时间安排
* 编辑、删除和暂停现有的计划电子邮件摘要

## 新建电子邮件摘要

1. 单击侧栏中的&#x200B;**[!DNL Manage Data]**，然后单击&#x200B;**[!UICONTROL Email Summary]**。

   如果这是您首次创建电子邮件摘要，则此页面不会显示任何已保存的摘要。

1. 单击右上角的&#x200B;**[!UICONTROL Create New Email Summary]**。

1. 输入摘要的名称。

   选择用于传达摘要中所包含内容的名称。 例如，`AOV Comparison`。

1. 在`Choose Content`部分中，选择要包含在摘要中的报告。

   您最多可以选择十个您拥有的报表。 选择报告后，使用显示的图标选择希望以表格或图表形式发送该报告。 如果将报表另存为数字，则只能将其作为数字发送。 有关发送包含包含过时数据报告的电子邮件摘要的信息，请参阅[管理帐户设置](../../administrator/account-management/managing-account-settings.md)。

   >[!NOTE]
   >
   >`Cohort`报告仅在您使用新架构时可用。

1. （可选）如果要接收电子邮件，请选择`Send Email To Me`。

1. 要在电子邮件中包括其他用户，请在`Add Email Recipients`字段中输入其电子邮件地址，该字段由逗号、空格、制表符或分号分隔。

## 计划电子邮件摘要

在`Set when to send the Email Summary`字段中，可以指定何时发送电子邮件摘要。 选项包括：

* `Manual`
* `Once`
* `Repeating`

### 保存稍后发送的电子邮件摘要

1. 从`Set when to send the Email Summary`字段中选择`Manual`。

1. 单击&#x200B;**[!UICONTROL Save]**。

   这会将摘要保存到电子邮件摘要列表中。

1. 准备好发送摘要时，单击齿轮图标并选择`Send Now`。

### 发送电子邮件摘要一次

1. 从`Set when to send the Email Summary`字段中选择`Once`。

1. 在`Select Start Date`日历中指定开始日期。

1. 在`Select time to send`字段中指定发送电子邮件的时间。

### 创建重复计划

1. 从`Set when to send the Email Summary`字段中选择`Repeating`。

1. 在`Set Frequency`字段中，选择`Daily`、`Weekly`或`Monthly`。

1. 在`Select Start Date`日历中指定开始日期。

1. 在`Select time to send`字段中指定发送电子邮件的时间。

1. （可选）要指定结束日期，请选择`End Date`并从日历中选择结束日期。

## 修改现有电子邮件摘要

创建并保存电子邮件摘要后，`Email Summaries`页面会显示所有已保存摘要的列表。 您可以展开每行(`+`)以了解详细信息。 此视图中的列为：

* `Email Name` — 电子邮件摘要的名称
* `Content` — 摘要中的内容类型，如任何报告的名称。 有关发送包含包含过时数据报告的电子邮件摘要的信息，请参阅[管理帐户设置](../../administrator/account-management/managing-account-settings.md)。
* `Scheduled` — 发送电子邮件摘要的频率、日期和时间
* `Recipients` — 电子邮件摘要的收件人
* `Created Date` — 创建电子邮件摘要的日期
* `Status` - `Paused`或`Active`

单击每行右侧的齿轮图标可以：

* `Send Now` — 立即向所有指定的收件人发送电子邮件摘要
* `Edit` — 允许您修改电子邮件摘要的详细信息
* `Pause/Active` — 允许您根据配置方式暂停发送电子邮件摘要或启用摘要
* `Delete` — 删除电子邮件摘要
