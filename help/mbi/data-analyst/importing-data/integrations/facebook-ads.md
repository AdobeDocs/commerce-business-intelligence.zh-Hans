---
title: 连接Facebook Ads
description: 学习分析广告支出数据，并查看您的资金是否得到了有效使用。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 连接 [!DNL Facebook Ads]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

你做了调查，做了广告，在网站上开展了活动 [!DNL Facebook]. 现在该分析您的广告支出数据了，看看您的资金是否得到了有效花销。 利用您的广告支出数据，您可以 [通过将您的广告成本和客户存留期价值(CLV)相结合来衡量促销活动ROI](../../../data-analyst/analysis/roi-ad-camp.md) 从营销活动获得的用户的数量。

正在连接您的 [!DNL Facebook Ad] 数据到 [!DNL Commerce Intelligence] 是一个简单的三步过程：

1. [添加 [!DNL Facebook] 作为中的数据源 [!DNL Commerce Intelligence]](#stepone)
1. [允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Facebook Ads] 数据](#steptwo)
1. [选择 [!DNL Facebook Ads] 用于提取数据的帐户](#stepthree)

## 添加 [!DNL Facebook] 作为中的数据源 [!DNL Commerce Intelligence] {#stepone}

1. 添加 [!DNL Facebook] 与您的集成 [!DNL Commerce Intelligence]帐户，导航到 `Connections` 页面位于 **[!UICONTROL Manage Data** > **Integrations]**.
1. 单击 **[!UICONTROL Add Integration]**，位于右侧。
1. 单击 [!DNL Facebook] 图标。 这会显示 [!DNL Facebook] 授权页面。
1. 单击 **[!UICONTROL Authorize]**.

## 允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Facebook Ads] 数据 {#steptwo}

单击后 **[!DNL Facebook Authorize]**，将显示一个小型弹出窗口：

![](../../../assets/Facebook_Access_Popup.png)

您需要执行一系列步骤以允许 [!DNL Commerce Intelligence] 要从公共个人资料访问数据，请执行以下操作： [!DNL Facebook Ads] 相关数据。 单击 **[!UICONTROL OK]** 执行这些步骤以继续。

## 选择 [!DNL Facebook Ads] 用于提取数据的帐户 {#stepthree}

1. 身份验证完成后，系统将提示您选择 [!DNL Facebook Ads] 要从中提取数据的帐户。 通过单击 `Connect` 列。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. 单击 **[!UICONTROL Save Connections]**.

   如果连接成功， *连接成功！* 消息将显示在页面顶部。

## 接下来呢？ {#next}

确保您正在跟踪 [!DNL Facebook] 中的营销活动 [!DNL Google Analytics]. 这可确保 `utm\_campaign` 中的字段 [!DNL Google Analytics] 已为您的正确填充 [!DNL Facebook] 营销活动。

## 相关

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [连接您的 [!DNL Google Adwords] 帐户](../integrations/google-ecommerce.md)
* [通过以下方式跟踪订单引用来源 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../../analysis/track-usr-dev-browser.md)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM归因工作？](../../analysis/utm-attributes.md)
