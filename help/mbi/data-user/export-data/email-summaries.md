---
title: 创建自动电子邮件摘要
description: 了解如何创建自动电子邮件摘要。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 创建自动电子邮件摘要

电子邮件摘要是一款功能强大的通信工具，可用于与关键利益相关方分享您业务的当前状态和趋势。 通过电子邮件摘要，您可以：

* 电子邮件图形摘要（包含报表）
* 包含或排除电子邮件摘要作者以接收电子邮件
* 安排发送电子邮件的时间
* 编辑、删除和暂停现有的计划电子邮件摘要

## 创建新电子邮件摘要

1. 单击 **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** 中。

   如果这是您首次创建电子邮件摘要，则此页面不会显示任何保存的摘要。

1. 单击 **[!UICONTROL Create New Email Summary]** 中。

1. 输入摘要的名称。

   选择传达摘要中包含的内容的名称。 例如， `AOV Comparison`.

1. 在 `Choose Content` 部分，选择要包含在摘要中的报表。

   您最多可以选择您拥有的10个报表。 选择报表后，使用显示的图标选择是否希望该报表作为表格或图表发送。 如果将报表保存为数字，则只能将其作为数字发送。 有关发送包含已过时数据报表的电子邮件摘要的信息，请参阅 [管理帐户设置](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` 报表仅在您使用新架构时才可用。

1. （可选）选择 `Send Email To Me` 要接收电子邮件。

1. 要在电子邮件中包含其他用户，请在 `Add Email Recipients` 字段中用逗号、空格、制表符或分号分隔。

## 计划电子邮件摘要

在 `Set when to send the Email Summary` 字段中，您可以指定发送电子邮件概要的时间。 选项包括：

* `Manual`
* `Once`
* `Repeating`

### 保存要在以后的日期发送的电子邮件摘要

1. 选择 `Manual` 从 `Set when to send the Email Summary` 字段。

1. 单击 **[!UICONTROL Save]**.

   这会将摘要保存到电子邮件摘要列表。

1. 准备好发送摘要后，单击齿轮图标，然后选择 `Send Now`.

### 发送电子邮件摘要一次

1. 选择 `Once` 从 `Set when to send the Email Summary` 字段。

1. 在 `Select Start Date` 日历。

1. 在 `Select time to send` 字段。

### 创建重复计划

1. 选择 `Repeating` 从 `Set when to send the Email Summary` 字段。

1. 在 `Set Frequency` 字段，选择 `Daily`, `Weekly`或 `Monthly`.

1. 在 `Select Start Date` 日历。

1. 在 `Select time to send` 字段。

1. （可选）要指定结束日期，请选择 `End Date` 并从日历中选择结束日期。

## 修改现有电子邮件摘要

创建并保存电子邮件摘要后， `Email Summaries` 页面显示所有保存的概要的列表。 您可以展开(`+`)每行以了解更多信息。 此视图中的列有：

* `Email Name`  — 电子邮件摘要的名称
* `Content`  — 摘要中的内容类型，如任何报表的名称。 有关发送包含已过时数据报表的电子邮件摘要的信息，请参阅 [管理帐户设置](../../administrator/account-management/managing-account-settings.md).
* `Scheduled`  — 发送电子邮件摘要的频率、日期和时间
* `Recipients`  — 电子邮件摘要的收件人
* `Created Date`  — 创建电子邮件摘要的日期
* `Status` - `Paused` 或 `Active`

单击每行右侧的齿轮图标可执行以下操作：

* `Send Now`  — 立即向所有指定收件人发送电子邮件摘要
* `Edit`  — 用于修改电子邮件摘要的详细信息
* `Pause/Active`  — 允许您暂停发送电子邮件摘要，或根据摘要的配置方式启用摘要
* `Delete`  — 删除电子邮件摘要
