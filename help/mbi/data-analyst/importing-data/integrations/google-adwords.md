---
title: 连接Google Adwords
description: 了解如何将您的广告成本与从您的促销活动中获得的用户的客户存留期价值(CLV)相结合，以衡量促销活动ROI。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 0%

---

# 连接[!DNL Google Adwords]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![Google AdWords徽标](../../../assets/Google_Adwords_logo.png)

您完成了调查，创建了广告，启动了[!DNL Google]营销活动。 现在该分析您的广告支出数据了，看看您的资金是否得到了有效花销。 使用广告支出数据，您可通过将广告成本和从营销活动中获得的用户的客户存留期价值(CLV) [相匹配来](../../analysis/roi-ad-camp.md)衡量营销活动ROI。

在[!DNL Google Adwords]中输入您的[!DNL Commerce Intelligence]凭据以开始操作。

1. 转到`Connections`管理数据>集成&#x200B;**下的**&#x200B;页面。
1. 单击屏幕右上角的&#x200B;**添加集成**。
1. 单击&#x200B;**[!DNL Google Adwords]**&#x200B;图标。 这将打开[!DNL Google Adwords]凭据页面。
1. 输入您的[!DNL Google Analytics]凭据。 授权过程完成后，您将被重定向回[!DNL Commerce Intelligence]。
1. 此时将显示配置文件ID列表。 检查要连接到[!DNL Commerce Intelligence]的配置文件。

   ![Google AdWords连接对话框显示配置文件选择](../../../assets/cnnct-profile.png)

1. 更改会自动保存，因此完成时请单击&#x200B;**[!UICONTROL Back to Connections]**。

如果您有多个用户档案并且需要帮助来识别哪个，请参阅下面的`Connecting Multiple Google Analytics profiles`部分。

## 连接多个[!DNL Google Analytics]配置文件

您可能将多个网站连接到单个[!DNL Google Analytics]帐户，并使用其自己的[!DNL Google Analytics]配置文件ID进行标识。 在这种情况下，您可以选择在[!DNL Commerce Intelligence]中包含您的所有配置文件ID。 选中要在用户档案选择步骤中包含的用户档案ID。

**要识别特定网站的Google Analytics配置文件ID：**

1. 登录[!DNL Google Analytics]
1. 转到特定网站的[!DNL Google Analytics]仪表板
1. 查看URL — 配置文件ID对应于行末尾位于`p`后面的八个数字：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 正在断开[!DNL Google Adwords]

1. 访问您的[!DNL Google] [帐户设置](https://www.google.com/account/about/?hl=en)页面。
1. 在`Security`部分下，单击&#x200B;**[!UICONTROL edit]**&#x200B;应用程序和站点旁边的`Authorizing`。
1. 单击&#x200B;**[!UICONTROL revoke access]**。

## 相关

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [通过 [!DNL Google ECommerce]跟踪订单反向链接来源](../integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../../analysis/google-track-user-acq.md)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM归因如何工作？](../../analysis/utm-attributes.md)
