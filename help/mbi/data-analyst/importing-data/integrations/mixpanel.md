---
title: 连接Mixpanel
description: 了解如何分析用户如何导航和使用您的网站和应用程序。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 连接[!DNL Mixpanel]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![](../../../assets/Mixpanel_logo.png)

通过[!DNL Mixpanel]，您可以分析用户如何导航和使用您的网站和应用。 仔细研究用户行为数据有助于做出更明智的设计和开发决策，这意味着总体产品会更好。 通过将[!DNL Mixpanel]连接到[!DNL Commerce Intelligence]，您可以分析用户的行为以及该行为如何转化为收入。

将您的[!DNL Mixpanel]数据连接到[!DNL Commerce Intelligence]一个简单的三步过程：

1. [在 [!DNL Mixpanel] 中打开 [!DNL Commerce Intelligence]凭据页面](#stepone)
1. [检索 [!DNL Mixpanel] API凭据](#steptwo)
1. [在 [!DNL Mixpanel] 中输入您的 [!DNL Commerce Intelligence]API凭据](#stepthree)

要完成此过程，您需要打开两个浏览器窗口或选项卡，一个用于[!DNL Commerce Intelligence]，另一个用于[!DNL Mixpanel]帐户。

## 正在打开[!DNL Mixpanel]凭据页面 {#stepone}

开始使用：

1. 转到`Connections`下的&#x200B;**[!DNL Manage Data** > **Connections]**&#x200B;页面。

1. 单击&#x200B;**[!UICONTROL Add a New Source]**，它位于屏幕右侧的`Data Sources`表上方。

1. 单击[!DNL Mixpanel]图标并打开凭据页面。

暂时保持此页面处于打开状态，并使用您的[!DNL Mixpanel]帐户切换到浏览器窗口。

## 正在检索您的[!DNL Mixpanel] API凭据 {#steptwo}

如果您尚未登录[!DNL Mixpanel]帐户，请登录，然后执行以下操作：

1. 单击右上角的&#x200B;**[!UICONTROL Account]**。

1. 在显示的对话框中，单击&#x200B;**[!UICONTROL Projects]**。

1. 您的API凭据显示：

![正在检索Mixpanel API凭据](../../../assets/Mixpanel_API_creds.png)

保持此打开状态，你需要它来结束此过程。

## 在[!DNL Mixpanel]中输入您的[!DNL Commerce Intelligence] API凭据 {#stepthree}

1. 将`API Key`和`Secret`复制到[!DNL Mixpanel]中的[!DNL Commerce Intelligence]凭据页面。
1. 单击&#x200B;**[!UICONTROL Connect to Mixpanel]**&#x200B;以完成设置。

如果连接成功，则&#x200B;_成功！_&#x200B;消息将显示在页面顶部。

### 相关

* [需要 [!DNL Mixpanel] 数据](../integrations/mixpanel-data.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hans)
