---
title: 管理Adobe Commerce用户和权限
description: 了解如何管理Commerce Intelligence用户。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 管理用户权限

[!DNL Adobe Commerce Intelligence] 旨在成为整个组织的单一真实来源。 每个用户都有自己的仪表板集，他们可以 [与其他用户共享](../../data-user/dashboards/share-dashboard-with-users.md).

## 用户权限级别

在 [!DNL Commerce Intelligence]，则有三个适用于用户的常规权限级别，这些级别在创建帐户时选择：

* `Admin`
* `Standard`
* `Read-Only`

这些权限使用户能够执行某些操作或访问的特定部分 [!DNL Commerce Intelligence]. 以下表格列出了每个权限级别在中可以执行的操作 [!DNL Commerce Intelligence]：

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **创建/管理用户** | ✔ |   |   |
| **创建电子邮件摘要** | ✔ | ✔ |   |
| **创建/编辑/共享功能板** | ✔ | ✔ |   |
| **查看仪表板** | ✔ | ✔ | ✔ |
| **创建/编辑/删除可视化报表** | ✔ | ✔* |   |
| **创建/编辑/删除SQL报告** | ✔ |  |   |
| **克隆功能板** | ✔ |   |   |
| **添加/管理集成** | ✔ |   |   |
| **访问Data Warehouse管理器** | ✔ |   |   |
| **同步/取消同步表和列** | ✔ |   |   |
| **创建/编辑量度** | ✔ |   |   |
| **创建/编辑过滤器集** | ✔ |   |   |
| **创建/编辑计算列** | ✔ |   |   |
| **创建依赖报表的列表** | ✔ |   |   |
| **访问系统摘要** | ✔ |   |   |
| **访问时区设置** | ✔ |   |   |
| **访问帐单** | ✔ | ✔** |   |
| **联系支持人员** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_您可以限制&#x200B;**[!UICONTROL Standard]**用户的 [访问特定量度](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _用户可以使用额外的权限设置访问账单。_
>
>**[!UICONTROL Read-Only]** 用户只能 _视图_ 已与他们共享的仪表板；他们无法在中创建或编辑任何内容 [!DNL Commerce Intelligence]，也无法搜索功能板并将其添加到帐户。 Adobe建议您与共享一组特定的功能板 **[!UICONTROL Read-Only]** 您或团队其他成员维护的用户。 请勿为其克隆一组功能板。

## 其他权限：账单和技术 {#billingtech}

除了一般权限级别之外，还有另外两个用户指定 —  `Billing` 和 `Technical`. 这些指定应与常规权限级别一起使用。

### 计费

`Billing` 用户有权访问计费页面，并可以更改付款信息。 此外，Adobe也可能联系他们以询问计费问题。

`Admin` 用户有权访问 `Billing` 制表符，但 `Standard` 如果用户具有 `Billing` 已选中此复选框。

![计费](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技术

`Technical` 用户没有任何特定于他们的权限 — 此设置仅标记组织内的技术联系人。 Adobe可能会就技术问题联系这些用户。

`Admin` 用户可以通过单击 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 并按照提示操作。 在中创建用户后 [!DNL Commerce Intelligence]，您邀请的幸运儿将收到有关如何完成帐户设置过程的电子邮件说明。

任何时候， `Admins` 可以通过单击查看其帐户中的所有用户 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. 此页面显示用户的权限以及他们可以访问的量度和功能板。
