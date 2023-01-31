---
title: Connect Zendesk
description: 了解如何在 [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 连接 [!DNL Zendesk]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

连接 [!DNL Zendesk] 通过数据，您可以整合 [!DNL MBI]. 这样，您就可以优化客户支持并监控服务台的绩效与收入。

连接 [!DNL Zendesk] 数据是一个简单的三步流程：

1. [打开 [!DNL Zendesk] 凭据页面 [!DNL MBI]](#stepone)
1. [检索 [!DNL Zendesk] API令牌](#steptwo)
1. [输入 [!DNL Zendesk] 登录信息和中的令牌 [!DNL MBI]](#stepthree)

要完成此过程，您需要打开两个浏览器窗口或选项卡 — 一个用于 [!DNL MBI]，另一个用于 [!DNL Zendesk] 帐户。

## 打开 [!DNL Zendesk] 凭据页面 [!DNL MBI] {#stepone}

1. 转到 `Integrations` 页面下 **[!UICONTROL Manage Data** > **&#x200B;数据源&#x200B;**> **集成]**.
1. 单击 **[!UICONTROL Add Integration]**，位于屏幕右侧。
1. 单击 [!DNL Zendesk] 图标。 这将打开 [!DNL Zendesk] 凭据页面。

## 检索 [!DNL Zendesk] API令牌 {#steptwo}

1. 在您登录的窗口/选项卡中 [!DNL Zendesk] 帐户，请单击屏幕左下角的设置（齿轮）图标。
1. 当 `Settings` 菜单，找到 `Channels` 中。 单击 **[!UICONTROL API]** 在此部分中。
1. 在 `Token Access` ，请单击此页面旁边的复选框 `Enabled`. 将显示活动API令牌列表。
1. 单击 **[!UICONTROL Add New Token]**.
1. 出现提示时，请输入令牌的标签。 我们建议使用 `MBI`，以便您一目了然地了解使用令牌的应用程序。
1. 单击 **[!UICONTROL Create]**.
1. 将创建API令牌。 复制此令牌；它将用在下一步中。

## 输入 [!DNL Zendesk] 登录信息和API令牌 [!DNL MBI] {#stepthree}

1. 输入 [!DNL Zendesk] 网站前缀和登录电子邮件 [!DNL Zendesk] 凭据页面 [!DNL MBI].
1. 输入API令牌。
1. 单击 **[!UICONTROL Save & Connect]**. 如果连接成功，则 *连接成功！* 消息将显示在屏幕顶部。

## 相关：

* [预期 [!DNL Zendesk] 数据](../integrations/exp-zendesk-data.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
