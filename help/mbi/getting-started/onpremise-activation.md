---
title: 激活 [!DNL MBI] 内部部署订阅帐户
description: 了解如何激活 [!DNL MBI] 内部部署订阅帐户。
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 激活 [!DNL MBI] 内部部署订阅帐户

激活 [!DNL MBI] 对于内部部署订阅，请先创建 [!DNL MBI] 帐户，然后连接 [!DNL MBI] 到您的商务数据库。 有关 `Cloud Starter` 项目，请参阅 [激活 [!DNL MBI] 帐户 `Cloud Starter` 订阅](../getting-started/cloud-activation.md).

1. 创建 [!DNL MBI] 帐户。

   - 转到 [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - 转到 **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - 单击 **[!UICONTROL Create Instance]**. 如果看不到此按钮，请联系您的客户成功经理或客户技术顾问。

   - 输入您的信息以创建帐户。

   ![](../assets/create-account-2.png)

   - 转到您的收件箱并验证您的电子邮件地址。 如果您没有收到电子邮件， [联系支持](../guide-overview.md).

   - 创建密码。

   ![](../assets/create-account-4.png)

   - 创建帐户后，您可以选择将用户添加到新帐户。 现在可以添加技术管理员以执行以下步骤。

   ![](../assets/create-account-5.png)

1. 输入有关商店的信息以设置首选项。

   ![](../assets/create-account-6.png)

1. 连接 [!DNL MBI] 使用加密连接到您的Commerce数据库。

   Commerce强烈建议您使用 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). 但是，如果这不是选项，您仍可以链接 [!DNL MBI] 使用 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. 成功连接后 [!DNL MBI] 要访问您的商务数据库，请联系您的客户成功经理以协调后续步骤，例如设置集成和其他配置步骤。

1. 完成配置后，您可以 [登录](../getting-started/sign-in.md) 至 [!DNL MBI] 帐户。
