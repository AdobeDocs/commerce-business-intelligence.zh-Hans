---
title: 连接Google E-commerce
description: 了解您最宝贵的转介渠道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 连接[!DNL Google ECommerce]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![](../../../assets/google-ecommerce-logo.png)

您拥有稳定的流量和订单流，这意味着您可以有效地联系和吸引客户。 但是，您最有价值的推荐渠道是什么？ 从一个来源获得的客户与从另一个来源获得的客户的平均生命周期值是多少？ 通过将您的订单引用源数据从[!DNL Google ECommerce]连接到[!DNL Commerce Intelligence]，您可以构建有助于您识别[最有价值的营销渠道](../../../data-analyst/analysis/most-value-source-channel.md)的分析。

在[!DNL Google ECommerce]中输入您的[!DNL Commerce Intelligence]凭据以开始操作：

1. 转到`Connections`下的&#x200B;**[!UICONTROL Admin** > **Connections]**&#x200B;页面。

1. 单击&#x200B;**[!UICONTROL Add a New Source]**，它位于屏幕右侧的`Data Sources`表上方。

1. 单击[!DNL Google ECommerce]图标。 这将打开[!DNL Google ECommerce]凭据页面。

1. 输入您的[!DNL Google Analytics]凭据。 授权过程完成后，您将被重定向回[!DNL Commerce Intelligence]。

1. 此时将显示配置文件ID列表。 检查要连接到[!DNL Commerce Intelligence]的配置文件。

   如果您有多个配置文件并且需要帮助来识别哪个，请参阅下面的**连接多个[!DNL Google Analytics]配置文件”部分。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 更改会自动保存，因此完成时请单击&#x200B;**[!UICONTROL Back to Connections]**。

## 将多个[!DNL Google Analytics]配置文件连接到[!DNL Commerce Intelligence]

您可能将多个网站连接到单个[!DNL Google Analytics]帐户，并使用其自己的[!DNL Google Analytics]配置文件ID进行标识。 在这种情况下，您可以选择在[!DNL Commerce Intelligence]中包含您的所有配置文件ID。 检查要在用户档案选择步骤中包含的用户档案ID。

要识别特定网站的[!DNL Google Analytics]配置文件ID，请执行以下操作：

1. 登录[!DNL Google Analytics]。
1. 转到特定网站的[!DNL Google Analytics]仪表板。
1. 查看URL — 配置文件ID对应于行末尾位于`p`后面的八个数字。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在断开[!DNL Google ECommerce]与[!DNL Commerce Intelligence]的连接 {#disconnect}

1. 访问您的[!DNL Google Analytics] [帐户设置](https://www.google.com/account/about/?hl=en)页面。
1. 在`Security`部分下，单击&#x200B;**[!UICONTROL edit]**&#x200B;应用程序和站点旁边的`Authorizing`。
1. 单击&#x200B;**[!UICONTROL revoke access]**&#x200B;旁边的[!DNL Commerce Intelligence]。

## 相关：

* [需要 [!DNL Google ECommerce] 数据](../integrations/google-ecommerce-data.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在设置 [!DNL Google ECommerce] 跟踪](https://support.google.com/analytics/answer/1009612?hl=en)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
