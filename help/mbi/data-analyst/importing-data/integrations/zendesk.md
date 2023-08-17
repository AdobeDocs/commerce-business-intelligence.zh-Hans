---
title: 连接Zendesk
description: 了解如何在中整合您的技术支持报告 [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# 连接 [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

正在连接您的 [!DNL Zendesk] 数据允许您在中整合技术支持报告 [!DNL Commerce Intelligence]. 这样，您就可以优化客户支持，并监控服务台绩效以及您的收入。

正在连接您的 [!DNL Zendesk] 数据是一个简单的三步过程：

1. [打开 [!DNL Zendesk] 凭据页面 [!DNL Commerce Intelligence]](#stepone)
1. [检索您的 [!DNL Zendesk] api令牌](#steptwo)
1. [输入您的 [!DNL Zendesk] 中的登录信息和令牌 [!DNL Commerce Intelligence]](#stepthree)

要完成此过程，您需要打开两个浏览器窗口或选项卡 — 一个用于 [!DNL Commerce Intelligence]，另一个用于 [!DNL Zendesk] 帐户。

## 打开 [!DNL Zendesk] 凭据页面 [!DNL Commerce Intelligence] {#stepone}

1. 转到 `Integrations` 页面位于 **[!UICONTROL Manage Data** > **&#x200B;数据源&#x200B;**> **集成]**.
1. 单击 **[!UICONTROL Add Integration]**，位于屏幕右侧。
1. 单击 [!DNL Zendesk] 图标。 这将打开 [!DNL Zendesk] “身份证明”页。

## 检索您的 [!DNL Zendesk] api令牌 {#steptwo}

1. 在登录到的窗口/选项卡中 [!DNL Zendesk] 帐户，单击屏幕左下角的设置（齿轮）图标。
1. 当 `Settings` 菜单显示，找到 `Channels` 部分。 单击 **[!UICONTROL API]** 在此部分中。
1. 在 `Token Access` 部分，单击旁边的复选框 `Enabled`. 此时将显示活动API令牌列表。
1. 单击 **[!UICONTROL Add New Token]**.
1. 出现提示时，输入令牌的标签。 Adobe建议使用 `Commerce Intelligence`，所以您一眼便知，使用令牌的应用程序有哪些。
1. 单击 **[!UICONTROL Create]**.
1. 创建API令牌。 复制此令牌；它将在下一步中使用。

## 输入 [!DNL Zendesk] 登录信息和API令牌进入 [!DNL Commerce Intelligence] {#stepthree}

1. 输入您的 [!DNL Zendesk] 网站前缀并登录电子邮件于 [!DNL Zendesk] 凭据页面 [!DNL Commerce Intelligence].
1. 输入您的API令牌。
1. 单击 **[!UICONTROL Save & Connect]**. 如果连接成功， *连接成功！* 消息显示在屏幕顶部。

## 相关：

* [预期 [!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
