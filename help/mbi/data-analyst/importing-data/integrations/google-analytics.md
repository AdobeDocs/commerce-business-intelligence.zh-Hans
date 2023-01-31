---
title: 连接Google Analytics
description: 了解如何将Google Analytics与 [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 连接 [!DNL Google Analytics]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是互联网上使用最广泛的Web分析服务。 实施 [!DNL Google Analytics] 通过网站上的，您可以跟踪访客如何使用您的网站、哪些内容很有吸引力、访客在哪里退出等。 在 [!DNL MBI]与其他数据一起，将提高网站的整体健康性和可用性。

让我们从进入 [!DNL Google Analytics] 凭据 [!DNL MBI]:

1. 转到 **[!UICONTROL Manage Data** > **Integrations]** 页面。
1. 单击 **[!UICONTROL Add Integration]**，位于屏幕右侧。
1. 单击 [!DNL Google Analytics] 图标。 这将打开 [!DNL Google Analytics] 凭据页面。
1. 输入 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL MBI].
1. 将显示配置文件ID列表。 检查要连接的用户档案 [!DNL MBI]. 如果您有多个用户档案，并且需要一些帮助来确定哪个是用户档案，请参阅连接多个 [!DNL Google Analytics] 用户档案部分。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 更改将自动保存，因此单击 **返回连接** 等你完成。

## 连接多个 [!DNL Google Analytics] 用户档案

您可能有多个网站连接到一个网站 [!DNL Google Analytics] 帐户，由其自己标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择在 [!DNL MBI]. 只需检查要在用户档案选择步骤中包含的用户档案ID即可。

确定特定网站的 [!DNL Google Analytics] 配置文件ID:

1. 登录 [!DNL Google Analytics]
1. 转到特定网站的 [!DNL Google Analytics] 仪表板
1. 查看URL — 配置文件ID对应于以下8个数字 `p` 在行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google Analytics] 从 [!DNL MBI] {#disconnect}

1. 访问 [!DNL Google Analytics] [帐户设置](https://www.google.com/accounts/) 页面。
1. 在 `Security` ，然后单击 **[!UICONTROL edit]** 下一页 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]** 下一页 [!DNL MBI].

## 相关：

* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
* [连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用跟踪用户获取数据 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
* [使用跟踪用户设备和浏览器数据 [!DNL Google Analytics] cookie](https://support.magento.com/hc/en-us/articles/360016732911)
