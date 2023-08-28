---
title: 激活您的 [!DNL Adobe Commerce Intelligence] 帐户
description: 了解联系谁来激活您的 [!DNL Commerce Intelligence] 帐户。
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 激活您的 [!DNL Commerce Intelligence] 本地和入门订阅帐户

激活 [!DNL Commerce Intelligence] 对于内部部署订阅，请首先创建 [!DNL Commerce Intelligence] 帐户，输入设置信息，然后连接 [!DNL Commerce Intelligence] 敬您的 [!DNL Commerce] 数据库。 <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## 创建您的 [!DNL Commerce Intelligence] 帐户

要创建您的帐户，请与您的Adobe客户团队或客户技术顾问联系。

## 创建密码

创建帐户后，请查看您的电子邮件中是否有来自的帐户通知电子邮件 [!DNL The Magento BI Team@rjmetrics.com]. 使用电子邮件中提供的链接访问 [!DNL Commerce Intelligence] 帐户并创建密码。 转到您的收件箱并验证您的电子邮件地址。

如果你没有收到电子邮件， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![](../assets/create-account-4.png)

## 设置您的商店首选项

在配置数据库连接之前，请填写存储信息表单。 需要此信息才能完成 **[!UICONTROL Connect your Database]** 设置。

![](../assets/create-account-6.png)

## 添加 [!DNL Commerce Intelligence] 用户

在设置密码并登录之后 [!DNL Commerce Intelligence]，您可以将其他用户添加到 [!DNL Commerce Intelligence] 帐户。 添加用户时，添加具有适当权限的管理用户以完成激活过程。

![](../assets/create-account-5.png)

## 创建专用 [!DNL Commerce Intelligence] 中的用户 [!DNL Commerce] 管理员

使用 [!DNL Commerce Intelligence]，您必须将永久和专用用户添加到 [!DNL Commerce] 项目。 此专用用户充当与 [!DNL Commerce] 支持获取新数据并将其传输到帐户的 [!DNL Commerce Intelligence] Data Warehouse。

配置专用 [!DNL Commerce Intelligence] 用户可确保不会停用或删除该帐户，从而停止 [!DNL Commerce Intelligence] 连接。


>[!NOTE]
>
>Adobe鼓励使用表明其永久状态的帐户名称（例如ACI-dedicated、ACI-database-connector等）。

在为创建专用用户之后 [!DNL Commerce Intelligence] 在“管理员”中，将同一用户添加到的主环境 [!DNL Commerce] 带有的项目 **[!UICONTROL Master]** 设置 `Contributor`.

![](../assets/commerce-add-user-settings.png)

## 获取Commerce Intelligence SSH密钥

1. 在 [!UICONTROL Connect your database] 第页对象 [!DNL Commerce Intelligence] 设置，向下滚动并选择 **[!UICONTROL Encryption settings]**.

1. 对象 **加密类型**，选择 `SSH Tunnel`.

1. 从下拉菜单中，复制提供的公共密钥。

   ![](../assets/encryption-setting-new-account.png)

## 将您的公钥添加到 [!DNL Commerce Intelligence]

1. 从 [!DNL Commerce Admin]，使用登录信息登录 [!DNL Commerce Intelligence] 您刚刚创建的用户。

1. 选择 **帐户设置** 选项卡。

1. 向下滚动并展开 **[!UICONTROL SSH Keys]** 下拉菜单。 然后，选择 **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. 将您复制的公钥粘贴到 [!DNL Encryption Type] 以上步骤。

   ![](../assets/paste-public-key.png)

## 提供 [!DNL Commerce Intelligence] Essentials `MySQL` 凭据

1. 更新您的 `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. 更新您的 `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## 获取数据库连接信息

将数据库连接信息获取到 [!DNL Commerce] 数据库至 [!DNL Commerce Intelligence]

1. 运行以下命令以获取您的信息。

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. 查看数据库信息，这些信息应该与以下示例类似。

   ![](../assets/example-database-information.png)

## 连接 [!DNL Commerce Intelligence] 敬您的 [!DNL Commerce] 使用加密连接的数据库

>[!NOTE]
>
>Adobe强烈建议您使用 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 用于建立数据库连接的隧道。 但是，如果无法使用此方法，您仍可以链接 [!DNL Commerce Intelligence] 到您的数据库 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

输入您的 [!DNL Commerce Intelligence] 中的信息 [!UICONTROL Connect your Magento Database] 屏幕。

![](../assets/connect-magento-db.png)

**输入：**

[!UICONTROL Integration Name]：[为您的选择一个名称， [!DNL Commerce Intelligence] 实例

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[！UICONTROL用户名]: `mbi`

[!UICONTROL Password]： [上一节中显示的输入密码]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]： [如果没有表前缀，则保留为空]

## 设置您的 [!UICONTROL **时区**] 设置

![](../assets/time-zone-settings.png)

**输入：**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]： [选择要显示数据的时区]

## 获取加密设置信息

项目UI提供SSH访问字符串。 此字符串可用于收集 [!UICONTROL **远程地址**] 和 [!UICONTROL **用户名**]. 通过在项目UI的主分支上选择访问站点按钮，使用SSH访问字符串。 然后，查找您的 [!UICONTROL User Name] 和 [!UICONTROL Remote Address] 如下所示。

![](../assets/master-branch-settings.png)

## 输入您的 [!DNL Encryption] 设置

![](../assets/encryption-settings-2.png)

**输入：**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]： `ssh.us-3.magento.cloud`  [自上一步]

[!UICONTROL Username]： `vfbfui4vmfez6-master-7rqtwti—mymagento`  [自上一步]

[!UICONTROL Port]: `22`

## 保存您的集成。

完成配置步骤后，通过选择以应用更改 [!UICONTROL **保存集成**].

您现在已成功连接 [!DNL Commerce] 数据库到您的 [!DNL Commerce Intelligence] 帐户。

>[!NOTE]
>
>如果您是 [!DNL Adobe Commerce Intelligence Pro] 联系您的客户成功经理或客户技术顾问以协调后续步骤。

完成配置后， [登录](../getting-started/sign-in.md) 敬您的 [!DNL Commerce Intelligence] 帐户。

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
