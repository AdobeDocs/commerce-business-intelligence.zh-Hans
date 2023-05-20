---
title: 连接 Google Analytics
description: 了解如何通过  [!DNL Commerce Intelligence] 连接 Google Analytics。
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 连接 [!DNL Google Analytics]

>[!NOTE]
>
>需要 [ 管理员权限 ](../../../administrator/user-management/user-management.md) 。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是 internet 上使用最广泛的网站分析服务。 通过在您的网站实施 [!DNL Google Analytics] ，您可以跟踪访客使用网站的方式、哪些内容有吸引力、访客退出的位置等。 在中 [!DNL Commerce Intelligence] 分析这些量度以及其他数据，可改进网站的整体运行状况和可用性。

将您 [!DNL Google Analytics] 的凭据输入到以下内容中 [!DNL Commerce Intelligence] 即可开始：

1. 转到 **[!UICONTROL Manage Data** > **Integrations]** 。

1. 单击 **[!UICONTROL Add Integration]** ，位于屏幕右侧。

1. [!DNL Google Analytics]单击图标。这会打开页面的 [!DNL Google Analytics] 凭据。

1. 输入您 [!DNL Google Analytics] 的凭据。 授权过程完成后，您将被重定向到 [!DNL Commerce Intelligence] 。

1. 显示列表的用户档案 Id。 检查要连接 [!DNL Commerce Intelligence] 的配置文件。 如果您有多个配置文件，并且需要一些帮助来识别哪些内容，请参阅下面的 &quot;连接多个 [!DNL Google Analytics] 配置文件&quot; 部分。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 更改会自动保存，因此在完成时单击 **返回连接** 。

## 连接多个 [!DNL Google Analytics] 配置文件

您可以将多个网站连接到单个 [!DNL Google Analytics] 帐户，并由其自身 [!DNL Google Analytics] 的用户档案 ID 进行标识。 在这种情况下，您可以选择将您的所有用户档案 Id 都包含在中 [!DNL Commerce Intelligence] 。 检查在 &quot;用户档案选择&quot; 步骤中要点赞包含的用户档案 Id。

识别特定网站的 [!DNL Google Analytics] 配置文件 ID：

1. 登录 [!DNL Google Analytics]
1. 转到特定网站的 [!DNL Google Analytics] 功能板
1. Look URL-配置文件 ID 对应于行尾后面 `p` 的八个数字：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google Analytics][!DNL Commerce Intelligence] {#disconnect}

1. 访问您的 [!DNL Google Analytics] [ 帐户设置 ](https://accounts.google.com/) 页面。
1. `Security`，然后单击 **[!UICONTROL edit]** &quot;应用程序和网站&quot; 旁边 `Authorizing` 的。
1. 单击 &quot;下一步 [!DNL Commerce Intelligence] &quot; **[!UICONTROL revoke access]** 。

## 相关：

* [Reauthenticating 集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用  [!DNL Google Analytics]  cookie 跟踪用户客户获取数据](../../analysis/google-track-user-acq.md)
