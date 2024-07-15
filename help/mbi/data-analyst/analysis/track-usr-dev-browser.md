---
title: Google Analytics — 跟踪数据库中的用户设备和浏览器数据
description: 了解有多少用户实际上通过移动设备登录，以及这如何影响这些用户的生命周期值。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!UICONTROL Google Analytics]跟踪

通过[!UICONTROL Google Analytics]，您可以[保存反向链接源信息](../analysis/google-track-user-acq.md)，以了解您最有价值的用户来自何处。 本主题讨论用户正在使用的平台（例如，设备或浏览器）。 通过它，您将能够了解有多少用户实际上通过移动设备登录，以及这如何影响这些用户的生命周期值。

## 保存用户设备和浏览器数据

每次向您的网站发出请求时，用户的浏览器都会发送一个User-Agent字符串，其中包含有关发出请求的平台的信息。 以下是User-Agent字符串的一些示例：

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

如果仔细查看，您会发现该字符串包含有关用户的操作系统、浏览器和用户正在使用的设备名称（如果该字符串具有名称）的信息。 尽管User-Agent字符串在各平台甚至同一平台的版本之间差别很大，但通常情况下，平台名称确实会存在于平台中的某个位置。 例如，上#1是带有Chrome浏览器的Mac，#2上是带有Firefox浏览器的Windows计算机，#3是iPhone，#4是iPad，#5是Android设备。

每次发出请求时，您的服务器都可以访问此信息。 在PHP中，用户代理字符串存储在`$_SERVER['HTTP_USER_AGENT']`中。 在Ruby on Rails中，它存储在`request.env['HTTP_USER_AGENT']`中。 其他语言和环境将允许您以类似方式访问它。

### 何时应记录此数据？

[!DNL Adobe]建议您将名为`Platform`或`User-Agent`的新字段添加到`Customers`和`Orders`数据库表，以便在创建用户或下达订单时存储此信息。 如果您使用的是SQL数据库，则此字段应为`VARCHAR(255)`。 

>[!NOTE]
>
>`User-Agent`字符串的长度允许远远超过此长度，但在实践中，它很少超过此长度。

### 如何解析有用的区段？

有许多库可帮助您将`User-Agent`字符串解析为操作系统、设备等组件。 请参阅[ua-parser项目](https://github.com/tobie/ua-parser)以了解详情。

有了这些新的信息，您可以更好地了解用户如何访问您的网站。 然后，您可以定制其体验或为特定组创建营销活动。

## 相关

* [通过 [!DNL Google Anaytics] E-Commerce跟踪订单反向链接来源](../importing-data/integrations/google-ecommerce.md)
* [跟踪数据库中的用户反向链接源](../analysis/google-track-user-acq.md)
* [了解您最有价值的客户获取来源和渠道](../analysis/most-value-source-channel.md)
* [连接你的 [!DNL Google Adwords] 帐户](../importing-data/integrations/google-adwords.md)
* [提高广告促销活动的ROI](../analysis/roi-ad-camp.md)
* [ [!DNL Google Analytics] UTM归因如何工作？](../analysis/utm-attributes.md)
