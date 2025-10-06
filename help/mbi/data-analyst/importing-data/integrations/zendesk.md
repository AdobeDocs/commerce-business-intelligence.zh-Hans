---
title: 连接Zendesk
description: 了解如何在 [!DNL Commerce Intelligence]中合并技术支持报告。
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 连接[!DNL Zendesk]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![Zendesk徽标](../../../assets/Zendesk_logo.png)

连接您的[!DNL Zendesk]数据允许您在[!DNL Commerce Intelligence]中合并技术支持报告。 这样，您就可以优化客户支持，并监控服务台绩效以及您的收入。

连接[!DNL Zendesk]数据是一个简单的三步过程：

1. [在 [!DNL Zendesk] 中打开 [!DNL Commerce Intelligence]凭据页面](#stepone)
1. [检索 [!DNL Zendesk] API令牌](#steptwo)
1. [在 [!DNL Zendesk] 中输入您的 [!DNL Commerce Intelligence]登录信息和令牌](#stepthree)

要完成此过程，您需要打开两个浏览器窗口或选项卡 — 一个用于[!DNL Commerce Intelligence]，另一个用于[!DNL Zendesk]帐户。

## 在[!DNL Zendesk]中打开[!DNL Commerce Intelligence]凭据页面 {#stepone}

1. 转到`Integrations`数据源&#x200B;**[!UICONTROL Manage Data** > ** > **集成&#x200B;**下的]**&#x200B;页面。
1. 单击屏幕右侧的&#x200B;**[!UICONTROL Add Integration]**。
1. 单击[!DNL Zendesk]图标。 这将打开[!DNL Zendesk]凭据页面。

## 检索您的[!DNL Zendesk] API令牌 {#steptwo}

1. 在您登录[!DNL Zendesk]帐户的窗口/选项卡中，单击屏幕左下角的设置（齿轮）图标。
1. 显示`Settings`菜单时，找到`Channels`部分。 单击此部分中的&#x200B;**[!UICONTROL API]**。
1. 在此页面的`Token Access`部分中，单击`Enabled`旁边的复选框。 此时将显示活动API令牌列表。
1. 单击&#x200B;**[!UICONTROL Add New Token]**。
1. 出现提示时，输入令牌的标签。 Adobe建议使用`Commerce Intelligence`，以便您一眼就能知道哪个应用程序正在使用令牌。
1. 单击&#x200B;**[!UICONTROL Create]**。
1. 创建API令牌。 复制此令牌；它将在下一步中使用。

## 在[!DNL Zendesk]中输入[!DNL Commerce Intelligence]登录信息和API令牌 {#stepthree}

1. 在[!DNL Zendesk]的[!DNL Zendesk]凭据页面中输入您的[!DNL Commerce Intelligence]站点前缀和登录电子邮件。
1. 输入您的API令牌。
1. 单击&#x200B;**[!UICONTROL Save & Connect]**。 如果连接成功，*连接成功！屏幕顶部显示*&#x200B;消息。

## 相关：

* [需要 [!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
