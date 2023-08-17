---
title: 连接Stripe
description: 了解如何管理和跟踪贵企业的付款和发票数据。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# 连接 [!DNL Stripe]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] 允许您管理和跟踪公司的付款和发票数据。 正在连接您的 [!DNL Stripe] 帐户至 [!DNL Commerce Intelligence] 是一个简单的两步流程：

1. [添加 [!DNL Stripe] 作为中的数据源 [!DNL Commerce Intelligence]](#stepone)
1. [允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Stripe] 数据](#steptwo)

## 添加 [!DNL Stripe] 作为数据源 {#stepone}

1. 转到 `Connections` 页面位于 **[!UICONTROL Admin** > **Connections]**.
1. 单击 **[!UICONTROL Add a Data Source]**，位于屏幕右侧上方的 `Data Sources` 表格。
1. 单击 [!DNL Stripe] 图标。 这会显示 `[!DNL Stripe] authorization` 页面。
1. 单击 **[!UICONTROL Connect with Stripe]**.

## 允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Stripe] 数据 {#steptwo}

单击后 **[!UICONTROL Connect with Stripe]**，则会显示访问请求页面。

1. 单击 **[!UICONTROL Sign in with Stripe to Continue]**.

1. 输入您的凭据，然后单击 **[!UICONTROL Sign in to your account]**.

1. 您的凭据将得到验证，并且您将被定向回 [!DNL Commerce Intelligence].

1. 如果连接成功， *连接成功！* 消息显示在屏幕顶部。

## 相关：

此 [[!DNL Stripe] API文档](https://stripe.com/docs/api) 可以成为详细了解如何操作的有用资源 [!DNL Stripe] 与集成 [!DNL Commerce Intelligence].

* [预期 [!DNL Stripe] 数据](../integrations/stripe-data.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
