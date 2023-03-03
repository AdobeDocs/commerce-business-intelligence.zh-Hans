---
title: 激活您的 [!DNL MBI] 用于内部部署订阅的帐户
description: 了解如何激活您的 [!DNL MBI] 用于内部部署订阅的帐户。
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 激活您的 [!DNL MBI] 用于内部部署订阅的帐户

激活 [!DNL MBI] 对于内部部署订阅，请首先创建 [!DNL MBI] 帐户，然后连接 [!DNL MBI] 到Commerce数据库。 有关在中激活的信息 `Cloud Starter` 项目，请参见 [激活您的 [!DNL MBI] 帐户 `Cloud Starter` 订阅](../getting-started/cloud-activation.md).

1. 创建您的 [!DNL MBI] 帐户。

   - 转到您的 [Adobe Commerce帐户登录](https://account.magento.com/customer/account/login)

   - 转到 **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - 单击 **[!UICONTROL Create Instance]**. 如果您没有看到此按钮，请与您的Adobe客户团队或客户技术顾问联系。

   - 输入您的信息以创建您的帐户。

   ![](../assets/create-account-2.png)

   - 转到收件箱并验证您的电子邮件地址。 如果你没有收到电子邮件， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - 创建密码。

   ![](../assets/create-account-4.png)

   - 创建帐户后，您可以选择将用户添加到新帐户。 现在可以添加技术管理员以执行以下步骤。

   ![](../assets/create-account-5.png)

1. 输入有关商店的信息以设置首选项。

   ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] 到您的Commerce数据库。

   Commerce强烈建议您使用 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). 但是，如果此选项不可用，您仍可以链接 [!DNL MBI] 到您的数据库，使用 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. 成功连接后 [!DNL MBI] 对于Commerce数据库，请联系您的Adobe客户团队以协调后续步骤，例如设置集成和其他配置步骤。

1. 完成配置后，您可以 [登录](../getting-started/sign-in.md) 敬您的 [!DNL MBI] 帐户。
