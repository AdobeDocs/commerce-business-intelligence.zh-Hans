---
title: 连接Stripe
description: 了解如何管理和跟踪贵企业的付款和发票数据。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 0%

---

# 连接[!DNL Stripe]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![Stripe徽标](../../../assets/stripe-logo.png)

[!DNL Stripe]允许您管理和跟踪公司的付款和发票数据。 将您的[!DNL Stripe]帐户连接到[!DNL Commerce Intelligence]是一个简单的两步过程：

1. [将 [!DNL Stripe] 添加为 [!DNL Commerce Intelligence]中的数据源](#stepone)
1. [允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Stripe] 数据](#steptwo)

## 将[!DNL Stripe]添加为数据源 {#stepone}

1. 转到`Connections`下的&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;页面。
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
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
