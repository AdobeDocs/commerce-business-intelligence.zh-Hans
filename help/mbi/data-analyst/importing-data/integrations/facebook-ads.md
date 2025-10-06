---
title: 连接Facebook广告
description: 学习分析广告支出数据，并查看您的资金是否得到了有效使用。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 连接[!DNL Facebook Ads]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![Facebook广告徽标](../../../assets/facebook-ads-logo.png)

你做了调查，做了广告，在[!DNL Facebook]上启动了你的营销活动。 现在该分析您的广告支出数据了，看看您的资金是否得到了有效花销。 使用广告支出数据，您可通过将广告成本和从营销活动中获得的用户的客户存留期价值(CLV) [相匹配来](../../../data-analyst/analysis/roi-ad-camp.md)衡量营销活动ROI。

将您的[!DNL Facebook Ad]数据连接到[!DNL Commerce Intelligence]是一个简单的三步过程：

1. [将 [!DNL Facebook] 添加为 [!DNL Commerce Intelligence]中的数据源](#stepone)
1. [允许 [!DNL Commerce Intelligence] 访问您的 [!DNL Facebook Ads] 数据](#steptwo)
1. [选择用于提取数据的 [!DNL Facebook Ads] 帐户](#stepthree)

## 将[!DNL Facebook]添加为[!DNL Commerce Intelligence]中的数据源 {#stepone}

1. 要将[!DNL Facebook]集成添加到您的[!DNL Commerce Intelligence]帐户，请导航到`Connections`下的&#x200B;**[!UICONTROL Manage Data** > **Integrations]**&#x200B;页面。
1. 单击右侧的&#x200B;**[!UICONTROL Add Integration]**。
1. 单击[!DNL Facebook]图标。 这将显示[!DNL Facebook]授权页面。
1. 单击&#x200B;**[!UICONTROL Authorize]**。

## 允许[!DNL Commerce Intelligence]访问您的[!DNL Facebook Ads]数据 {#steptwo}

单击&#x200B;**[!DNL Facebook Authorize]**&#x200B;后，将显示一个小型弹出窗口：

Commerce Intelligence的![Facebook访问权限对话框](../../../assets/Facebook_Access_Popup.png)

您按照一系列步骤操作，以允许[!DNL Commerce Intelligence]访问您的公共个人资料、[!DNL Facebook Ads]和相关统计信息中的数据。 单击这些步骤中的&#x200B;**[!UICONTROL OK]**&#x200B;以继续。

## 选择用于提取数据的[!DNL Facebook Ads]帐户 {#stepthree}

1. 身份验证完成后，系统将提示您选择要从中提取数据的[!DNL Facebook Ads]帐户。 通过单击`Connect`列中的复选框选择所需的帐户。

   ![Facebook广告帐户选择界面](../../../assets/Facebook_Ad_Accounts.png)

1. 单击&#x200B;**[!UICONTROL Save Connections]**。

   如果连接成功，*连接成功！*&#x200B;消息将显示在页面顶部。

## 接下来呢？ {#next}

确保您在[!DNL Facebook]中跟踪[!DNL Google Analytics]营销活动。 这可确保为您的`utm\_campaign`营销活动正确填充[!DNL Google Analytics]中的[!DNL Facebook]字段。

## 相关

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
* [连接你的 [!DNL Google Adwords] 帐户](../integrations/google-ecommerce.md)
* [通过 [!DNL Google eCommerce]跟踪订单反向链接来源](../integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../../analysis/google-track-user-acq.md)
* [跟踪数据库中的用户设备、浏览器和操作系统数据](../../analysis/track-usr-dev-browser.md)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM归因如何工作？](../../analysis/utm-attributes.md)
