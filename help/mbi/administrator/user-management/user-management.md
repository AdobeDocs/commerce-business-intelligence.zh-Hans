---
title: 管理用户和权限
description: 了解如何管理 [!DNL MBI] 用户。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 管理用户权限

MBI旨在成为整个组织中唯一的真相来源。 每个用户都将拥有自己的功能板集，他们可以 [与其他用户共享](../../data-user/dashboards/share-dashboard-with-users.md).

## 用户权限级别

在 [!DNL MBI]，则有三个适用于用户的一般权限级别，在创建帐户时，将会选择这些级别：

* `Admin`
* `Standard`
* `Read-Only`

这些权限允许用户执行某些操作或访问 [!DNL MBI]. 下面是每个权限级别在MBI中可以执行的操作的表：

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **创建/管理用户** | ✔ |  |  |
| **创建电子邮件摘要** | ✔ | ✔ |  |
| **创建/编辑/共享功能板** | ✔ | ✔ |  |
| **查看功能板** | ✔ | ✔ | ✔ |
| **创建/编辑/删除可视化报表** | ✔ | ✔* |  |
| **创建/编辑/删除SQL报告** | ✔ |  |  |
| **克隆功能板** | ✔ |  |  |
| **添加/管理集成** | ✔ |  |  |
| **访问Data warehouse管理器** | ✔ |  |  |
| **同步/不同步表和列** | ✔ |  |  |
| **创建/编辑量度** | ✔ |  |  |
| **创建/编辑过滤器集** | ✔ |  |  |
| **创建/编辑计算列** | ✔ |  |  |
| **创建从属报表列表** | ✔ |  |  |
| **访问系统摘要** | ✔ |  |  |
| **访问时区设置** | ✔ |  |  |
| **访问帐单** | ✔ | ✔** |  |
| **联系支持人员** | ✔ | ✔ | ✔ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>_您可以限制&#x200B;**[!UICONTROL Standard]**用户 [访问特定量度](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _用户可以通过其他权限设置访问账单。_
>
>**[!UICONTROL Read-Only]** 用户只能 _视图_ 与其共享的功能板；无法在 [!DNL MBI]，则用户也无法搜索新功能板并将其添加到其帐户。 我们建议您与 **[!UICONTROL Read-Only]** 您或团队其他成员维护的用户。 请勿为其克隆功能板集。

## 其他权限：计费和技术 {#billingtech}

除了一般权限级别之外，还存在另外两个用户名称 —  `Billing` 和 `Technical`. 这些指定将与一般权限级别结合使用。

### 帐单

`Billing` 用户有权访问帐单页面，并可以更改付款信息。 此外，我们的团队也可能会联系他们，以了解有关账单的问题。

`Admin` 默认情况下，用户有权访问“帐单”选项卡，但是如果标准用户具有 `Billing` 复选框。

![计费](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技术

`Technical` 用户没有任何特定权限 — 此设置只会标记您组织内的技术联系人。 我们的团队可能会就技术问题联系这些用户。

`Admin` 用户可以通过单击 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 并按提示操作。 在中创建用户后 [!DNL MBI]，您邀请的幸运者将收到有关如何完成帐户设置过程的电子邮件说明。

随时， `Admins` 可通过单击 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. 此页面显示用户的权限以及他们有权访问的量度和功能板。
