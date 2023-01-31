---
title: 连接条带
description: 了解如何管理和跟踪您企业的付款和发票数据。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 连接条带

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] 允许您管理和跟踪业务的付款和发票数据。 连接 [!DNL Stripe] 帐户 [!DNL MBI] 是一个简单的两步流程：

1. [添加 [!DNL Stripe] 作为 [!DNL MBI]](#stepone)
1. [允许 [!DNL MBI] 访问 [!DNL Stripe] 数据](#steptwo)

## 添加 [!DNL Stripe] 作为数据源 {#stepone}

1. 转到 `Connections` 页面下 **[!UICONTROL Admin** > **Connections]**.
1. 单击 **[!UICONTROL Add a Data Source]**，位于屏幕右侧，位于 `Data Sources` 表。
1. 单击 [!DNL Stripe] 图标。 这将显示 `[!DNL Stripe] authorization` 页面。
1. 单击 **[!UICONTROL Connect with Stripe]**.

## 允许 [!DNL MBI] 访问 [!DNL Stripe] 数据 {#steptwo}

单击 **[!UICONTROL Connect with Stripe]**，则会显示访问请求页面。

1. 单击 **[!UICONTROL Sign in with Stripe to Continue]**.

1. 输入您的凭据并单击 **[!UICONTROL Sign in to your account]**.

1. 单击后，将验证您的凭据，并将您定向回 [!DNL MBI].

1. 如果连接成功，则 *连接成功！* 消息将显示在屏幕顶部。

## 相关：

如果你更懂技术，那么 [[!DNL Stripe] API文档](https://stripe.com/docs/api) 可以作为有用资源，进一步了解 [!DNL Stripe] 与 [!DNL MBI].

* [预期 [!DNL Stripe] 数据](../integrations/stripe-data.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
