---
title: 连接Mixpanel
description: 了解如何分析用户如何导航和使用您的网站和应用程序。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

替换为 [!DNL Mixpanel]，您可以分析用户如何导航和使用您的网站和应用程序。 仔细研究用户行为数据有助于做出更明智的设计和开发决策，这意味着总体产品会更好。 正在连接 [!DNL Mixpanel] 到 [!DNL MBI] 可让您分析用户的行为以及该行为如何转化为收入。

正在连接 [!DNL Mixpanel] 数据到 [!DNL MBI] 一个简单的三步流程：

1. [打开 [!DNL Mixpanel] 凭据页面 [!DNL MBI]](#stepone)
1. [检索您的 [!DNL Mixpanel] API凭据](#steptwo)
1. [输入您的 [!DNL Mixpanel] MBI中的API凭据](#stepthree)

要完成此过程，您需要打开两个浏览器窗口或选项卡 — 一个用于 [!DNL MBI]，其他代表您的 [!DNL Mixpanel] 帐户。

## 打开 [!DNL Mixpanel] “身份证明”页 {#stepone}

开始使用：

1. 转到 `Connections` 页面位于 **[!DNL Manage Data** > **Connections]**.
1. 单击 **[!UICONTROL Add a New Source]**，位于屏幕右侧上方的 `Data Sources` 表格。
1. 单击 [!DNL Mixpanel] 图标和凭据页面打开。

暂时保持此页面处于打开状态，然后使用切换到浏览器窗口 [!DNL Mixpanel] 帐户。

## 正在检索您的 [!DNL Mixpanel] API凭据 {#steptwo}

如果您尚未登录 [!DNL Mixpanel] 尚未帐户，请执行上述操作，然后执行以下操作：

1. 单击 **[!UICONTROL Account]** 在右上角。
1. 在显示的对话框中，单击 **[!UICONTROL Projects]**.
1. 此时将显示您的API凭据：

![正在检索Mixpanel API凭据](../../../assets/Mixpanel_API_creds.png)

保持此打开 — 您需要它来结束此操作。

## 输入您的 [!DNL Mixpanel] 中的API凭据 [!DNL MBI] {#stepthree}

1. 复制 `API Key` 和 `Secret` 到 [!DNL Mixpanel] 凭据页面 [!DNL MBI].
1. 单击 **[!UICONTROL Connect to Mixpanel]** 以完成设置。

就是这样！ 如果连接成功， _成功！_ 消息将显示在页面顶部。

### 相关

* [预期 [!DNL Mixpanel] 数据](../integrations/mixpanel-data.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
