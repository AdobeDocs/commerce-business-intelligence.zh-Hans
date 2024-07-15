---
title: 连接Stripe
description: 了解如何管理和跟踪贵企业的付款和发票数据。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 连接[!DNL Stripe]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![](../../../assets/stripe-logo.png)

[!DNL Stripe]允许您管理和跟踪公司的付款和发票数据。 将您的[!DNL Stripe]帐户连接到[!DNL Commerce Intelligence]是一个简单的两步过程：

1. [将 [!DNL Stripe] 添加为 [!DNL Commerce Intelligence]中的数据源](#stepone)
1. [允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Stripe] 数据](#steptwo)

## 将[!DNL Stripe]添加为数据源 {#stepone}

1. 转到&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;下的`Connections`页面。
1. 单击&#x200B;**[!UICONTROL Add a Data Source]**，它位于屏幕右侧的`Data Sources`表上方。
1. 单击[!DNL Stripe]图标。 这会显示`[!DNL Stripe] authorization`页面。
1. 单击&#x200B;**[!UICONTROL Connect with Stripe]**。

## 允许[!DNL Commerce Intelligence]访问您的[!DNL Stripe]数据 {#steptwo}

单击&#x200B;**[!UICONTROL Connect with Stripe]**&#x200B;后，将显示访问请求页面。

1. 单击&#x200B;**[!UICONTROL Sign in with Stripe to Continue]**。

1. 输入您的凭据，然后单击&#x200B;**[!UICONTROL Sign in to your account]**。

1. 将验证您的凭据，并将您定向回[!DNL Commerce Intelligence]。

1. 如果连接成功，*连接成功！屏幕顶部显示*&#x200B;消息。

## 相关：

[[!DNL Stripe] API文档](https://stripe.com/docs/api)可以成为了解有关[!DNL Stripe]如何与[!DNL Commerce Intelligence]集成的有用资源。

* [需要 [!DNL Stripe] 数据](../integrations/stripe-data.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
