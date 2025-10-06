---
title: 连接数据
description: 了解如何在Data Warehouse Manager中浏览可用于同步的表。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# 连接数据

在[!DNL Adobe Commerce Intelligence]中，数据源称为`integrations`。 成功连接`integration`后，您将能够在Data Warehouse管理器中浏览可用于同步的表。

使用`Connections`页面添加和管理集成，单击&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;可访问该页面。 在这里，您会看到：

* 连接到您帐户的所有集成的列表

* 集成类型

* 状态（[!DNL Google Analytics]和[!DNL Data Import API]连接的状态字段为空）

* 上次执行连接测试（`Last Connection Started`列）的时间

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 集成类型

有四种方法可将数据导入[!DNL Commerce Intelligence]：连接数据库、连接SaaS集成、上传`.csv`文件或使用Adobe API。

## 数据库集成

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence]支持基于SQL和NoSQL的数据库，如[MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md)、[Microsoft SQL](../integrations/microsoft-sql-server.md)、[MongoDB](../integrations/mongodb-via-ssh-tunnel.md)和[PostgreSQL](../integrations/postgresql.md)。

虽然您可以使用数据库凭据直接将数据库连接到[!DNL Commerce Intelligence]，但Adobe建议您使用经验证的加密方法，如SSH通道。 这可确保数据在进入Data Warehouse时保持安全和安全。

根据连接方法和数据库类型，可能需要一些技术专家才能完成设置。

## `SaaS`集成

![显示各种受支持平台的SaaS集成图标](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS`集成是诸如[[!DNL Google Adwords]](../integrations/google-adwords.md)、[[!DNL Salesforce]](../integrations/salesforce.md)和[[!DNL Zendesk]](../integrations/zendesk.md)之类的服务。 由于第三方数据位于供应商的服务器上，因此您不能像使用数据库中的数据那样直接访问这些数据。

通常，在[!DNL Commerce Intelligence]中设置集成与只需输入帐户凭据一样简单。 某些服务可能需要API密钥才能完成授权。 有关生成您需要的任何凭据的说明，请查看[集成部分](../integrations/integrations.md)。

## 文件上传

不确定如何将数据从补充源纳入您的Data Warehouse？ [使用`File Upload`功能](../connecting-data/using-file-uploader.md)是一种拉入数据的好方法，您在日常决策中不需要这些数据。 按照格式规则，您可以快速将`.csv`文件上传到Data Warehouse并将其与其他数据源联接。

## [!DNL Commerce Intelligence] `Import API`

如果您希望从您自己的来源中自动检索数据，则可以使用[!DNL Commerce Intelligence] `Import API`。 基本上，如果它不在数据库或`SaaS`集成中，则`Import API`函数是您的最佳选择。

使用API需要一点技术专业知识 — 能够熟练编写和维护小型Ruby或PHP脚本的人非常符合条件。

若要了解有关`Import API`入门的更多信息，请查看[开发人员网站](https://developer.adobe.com/commerce/services/reporting/)和[如何生成API密钥](https://developer.adobe.com/commerce/services/reporting/import-api/)。

## 添加集成

要添加集成，请单击&#x200B;**[!UICONTROL Manage Data** > **Connections]**，然后单击&#x200B;**[!UICONTROL Add a New Data Source]**。 单击要添加集成的图标，然后按照帮助主题中的说明进行设置：

* [集成常见问题解答](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [可用 &#x200B;](../integrations/integrations.md)
* [合并表](../../../best-practices/consolidating-your-tables.md)
* [限制对数据库的访问](../../../administrator/account-management/restrict-db-access.md)

**没有看到您想要的集成？**&#x200B;必须激活某些集成，才会在您的帐户中显示。 如果您要查找诸如[!DNL Facebook]之类的内容，但该内容未列出，请[提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

**如果看到集成**&#x200B;的错误状态，请查看[疑难解答部分](https://support.magento.com/hc/en-us/sections/360003078151)以获取帮助。
