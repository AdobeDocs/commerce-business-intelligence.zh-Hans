---
title: 連線Zendesk
description: 瞭解如何在中整合您的服務檯報告 [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

[!DNL Zendesk]通过连接您的数据，您可以在中整合您的 [!DNL Commerce Intelligence] 服务台报告。这允许您优化客户支持和监测服务台性能及收入。

[!DNL Zendesk]连接数据是一个简单的三步过程：

1. [ [!DNL Zendesk] 在中打开凭据页面 [!DNL Commerce Intelligence]](#stepone)
1. [检索您的  [!DNL Zendesk]  API 令牌](#steptwo)
1. [在中输入您  [!DNL Zendesk]  的登录信息和令牌 [!DNL Commerce Intelligence]](#stepthree)

要完成此过程，您需要为您 [!DNL Zendesk] 的帐户打开两个浏览器窗口或选项卡（一个 [!DNL Commerce Intelligence] ）。

## [!DNL Zendesk]在中打开凭据页面[!DNL Commerce Intelligence] {#stepone}

1. 前往 `Integrations` 頁面於 **[!UICONTROL Manage Data** > **&#x200B;資料來源&#x200B;**> **整合]**.
1. 按一下 **[!UICONTROL Add Integration]**，位於熒幕右側。
1. 按一下 [!DNL Zendesk] 圖示。 如此將可開啟 [!DNL Zendesk] 認證頁面。

## 检索您的 [!DNL Zendesk] API 令牌 {#steptwo}

1. 在您登录 [!DNL Zendesk] 帐户的窗口/选项卡中，单击屏幕左下角的 &quot;设置（齿轮）&quot; 图标。
1. `Settings`显示菜单时，请找到 `Channels` 相应的部分。单击 **[!UICONTROL API]** 此部分。
1. `Token Access`在此页面部分，单击旁边 `Enabled` 的复选框。显示活动 API 令牌的列表。
1. 单击 **[!UICONTROL Add New Token]** 。
1. 出现提示时，输入令牌的标签。 Adobe Systems 建议使用 `Commerce Intelligence` ，您可以一目了然地了解使用令牌的应用程序。
1. 按一下 **[!UICONTROL Create]**.
1. 已建立API權杖。 複製此Token；它將在下一個步驟中使用。

## 輸入 [!DNL Zendesk] 登入資訊和API權杖登入 [!DNL Commerce Intelligence] {#stepthree}

1. 输入您 [!DNL Zendesk] 的 [!DNL Zendesk] 网站前缀，并在页面 [!DNL Commerce Intelligence] 的凭据中登录电子邮件。
1. 输入您的 API 令牌。
1. 单击 **[!UICONTROL Save & Connect]** 。 如果连接成功， *则连接成功！* 消息显示在屏幕顶部。

## 相关：

* [预期  [!DNL Zendesk]  数据](../integrations/exp-zendesk-data.md)
* [Reauthenticating 集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
