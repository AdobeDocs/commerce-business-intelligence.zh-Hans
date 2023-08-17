---
title: 连接Google Adwords
description: 了解如何将您的广告成本与从您的促销活动中获得的用户的客户存留期价值(CLV)相结合，以衡量促销活动ROI。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 连接 [!DNL Google Adwords]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

你做了调查，做了广告，启动了 [!DNL Google] 营销活动。 现在该分析您的广告支出数据了，看看您的资金是否得到了有效花销。 利用您的广告支出数据，您可以 [通过将您的广告成本和客户存留期价值(CLV)相结合来衡量促销活动ROI](../../analysis/roi-ad-camp.md) 从营销活动获得的用户的数量。

通过输入您的 [!DNL Google Adwords] 凭据进入 [!DNL Commerce Intelligence].

1. 转到 `Connections` 页面位于 **管理数据>集成**.
1. 单击 **添加集成**，位于屏幕右上角。
1. 单击 **[!DNL Google Adwords]** 图标。 这将打开 [!DNL Google Adwords] “身份证明”页。
1. 输入您的 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL Commerce Intelligence].
1. 此时将显示配置文件ID列表。 检查要连接的配置文件 [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. 更改会自动保存，因此请单击 **[!UICONTROL Back to Connections]** 完成时。

如果您有多个用户档案并且需要帮助来识别哪个，请参阅 `Connecting Multiple Google Analytics profiles` 部分。

## 连接多个 [!DNL Google Analytics] 用户档案

您可能已将多个网站连接到单个 [!DNL Google Analytics] 帐户，由其自身的标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择将您的所有配置文件ID包含在 [!DNL Commerce Intelligence]. 选中要在用户档案选择步骤中包含的用户档案ID。

**要识别特定网站的Google Analytics配置文件ID，请执行以下操作：**

1. 登录 [!DNL Google Analytics]
1. 前往特定网站的 [!DNL Google Analytics] 仪表板
1. 查看URL — 配置文件ID对应于以下八个数字 `p` 行尾：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 断开连接 [!DNL Google Adwords]

1. 访问您的 [!DNL Google] [帐户设置](https://www.google.com/account/about/?hl=en) 页面。
1. 在 `Security` 部分，单击 **[!UICONTROL edit]** 旁边 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]**.

## 相关

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [通过以下方式跟踪订单引用来源 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../../analysis/google-track-user-acq.md)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM归因工作？](../../analysis/utm-attributes.md)
