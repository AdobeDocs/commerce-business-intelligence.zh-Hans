---
title: 连接数据
description: 了解如何在Data Warehouse管理器中浏览可用于同步的表。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 连接数据

在 [!DNL Adobe Commerce Intelligence]，数据源称为 `integrations`. 之后 `integration` 已成功连接，您将能够在Data Warehouse管理器中浏览可用于同步的表。

可使用添加和管理集成 `Connections` 页面，单击可访问该页面 **[!UICONTROL Manage Data** > **Connections]**. 在这里，您会看到：

* 连接到您帐户的所有集成的列表

* 集成类型

* 状态([!DNL Google Analytics] 和 [!DNL Data Import API] 连接状态字段为空)

* 上次连接测试的时间(`Last Connection Started` （列）的操作已执行

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 集成类型

有四种方法可将您的数据导入 [!DNL Commerce Intelligence]：连接数据库、连接SaaS集成、上载 `.csv` 文件，或使用AdobeAPI。

## 数据库集成

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] 支持基于SQL和NoSQL的数据库，例如 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md)， [MICROSOFT SQL](../integrations/microsoft-sql-server.md)， [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)、和 [PostgreSQL](../integrations/postgresql.md).

虽然您可以直接将数据库连接到 [!DNL Commerce Intelligence] 使用数据库凭据，Adobe建议您使用经验证的加密方法，如SSH通道。 这可确保在数据进入Data Warehouse时保持安全和安全。

根据连接方法和数据库类型，可能需要一些技术专家才能完成设置。

## `SaaS` 集成

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 集成是类似以下的服务 [[!DNL Google Adwords]](../integrations/google-adwords.md)， [[!DNL Salesforce]](../integrations/salesforce.md)、和 [[!DNL Zendesk]](../integrations/zendesk.md). 由于第三方数据位于供应商的服务器上，因此您不能像使用数据库中的数据那样直接访问这些数据。

通常，在中设置集成 [!DNL Commerce Intelligence] 就像只需输入帐户凭据一样简单。 某些服务可能需要API密钥才能完成授权。 查看 [“集成”部分](../integrations/integrations.md) 以获取有关生成您需要的任何凭据的说明。

## 文件上传

不确定如何将数据从补充源纳入您的Data Warehouse？ [使用 `File Upload` 特征](../connecting-data/using-file-uploader.md) 是一种拉入数据的好方法，您在日常决策中不需要这些数据。 按照格式规则，您可以快速上传 `.csv` 将文件加入Data Warehouse中，并将其与其他数据源联接。

## [!DNL Commerce Intelligence] `Import API`

如果您希望自动检索您自己的某个源中的数据，则可以使用 [!DNL Commerce Intelligence] `Import API`. 基本上，如果它不在数据库或 `SaaS` 集成， `Import API` 功能是你的最佳选择。

使用API需要一点技术专业知识 — 能够熟练编写和维护小型Ruby或PHP脚本的人非常符合条件。

要了解有关入门的更多信息，请参阅 `Import API`，查看 [开发人员网站](https://developer.adobe.com/commerce/services/reporting/) 和 [如何生成API密钥](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 添加集成

要添加集成，请单击 **[!UICONTROL Manage Data** > **Connections]** 然后单击 **[!UICONTROL Add a New Data Source]**. 单击要添加集成的图标，然后按照帮助主题中的说明进行设置：

* [集成常见问题解答](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [可用 ](../integrations/integrations.md)
* [合并表](../../../best-practices/consolidating-your-tables.md)
* [限制对数据库的访问](../../../administrator/account-management/restrict-db-access.md)

**没有看到您想要的集成？** 必须激活某些集成，才会在您的帐户中显示。 如果您要查找 [!DNL Facebook] 但并未列出， [提交支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**如果您看到集成的错误状态**，查看 [“疑难解答”部分](https://support.magento.com/hc/en-us/sections/360003078151) 以寻求帮助。
