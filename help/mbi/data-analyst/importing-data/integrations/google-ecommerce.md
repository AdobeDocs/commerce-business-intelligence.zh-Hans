---
title: 连接Google电子商务
description: 了解您最宝贵的推荐渠道。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

您拥有稳定的流量和订单流，这意味着您可以有效地联系和吸引客户。 但您最有价值的推荐渠道是什么？ 从一个来源获得的客户与从另一个来源获得的客户的平均生命周期值是多少？ 通过连接您的订单反向链接源数据 [!DNL Google ECommerce] 到 [!DNL Commerce Intelligence]，您可以构建分析来帮助您识别 [最有价值的营销渠道](../../../data-analyst/analysis/most-value-source-channel.md).

通过输入您的 [!DNL Google ECommerce] 凭据进入 [!DNL Commerce Intelligence]：

1. 转到 `Connections` 页面位于 **[!UICONTROL Admin** > **Connections]**.

1. 单击 **[!UICONTROL Add a New Source]**，位于屏幕右侧上方的 `Data Sources` 表格。

1. 单击 [!DNL Google ECommerce] 图标。 这将打开 [!DNL Google ECommerce] “身份证明”页。

1. 输入您的 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL Commerce Intelligence].

1. 此时将显示配置文件ID列表。 检查要连接的配置文件 [!DNL Commerce Intelligence].

   如果您有多个用户档案，并且需要一些帮助来识别哪个是哪个，请参阅**连接多个 [!DNL Google Analytics] 配置文件部分。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 更改会自动保存，因此请单击 **[!UICONTROL Back to Connections]** 等你完事了。

## 连接多个 [!DNL Google Analytics] 配置文件至 [!DNL Commerce Intelligence]

您可能已将多个网站连接到一个 [!DNL Google Analytics] 帐户，由其自身标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择将您的所有配置文件ID包含在 [!DNL Commerce Intelligence]. 检查要在用户档案选择步骤中包含的用户档案ID。

识别特定网站的 [!DNL Google Analytics] 配置文件ID：

1. 登录 [!DNL Google Analytics].
1. 前往特定网站的 [!DNL Google Analytics] 仪表板。
1. 查看URL — 配置文件ID对应于以下八个数字 `p` 在行尾。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google ECommerce] 起始日期 [!DNL Commerce Intelligence] {#disconnect}

1. 访问您的 [!DNL Google Analytics] [帐户设置](https://www.google.com/account/about/?hl=en) 页面。
1. 在 `Security` 部分，单击 **[!UICONTROL edit]** 旁边 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]** 旁边 [!DNL Commerce Intelligence].

## 相关：

* [预期 [!DNL Google ECommerce] 数据](../integrations/google-ecommerce-data.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [设置 [!DNL Google ECommerce] 跟踪](https://support.google.com/analytics/answer/1009612?hl=en)
* [了解您最有价值的客户获取来源和渠道](../../analysis/most-value-source-channel.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
