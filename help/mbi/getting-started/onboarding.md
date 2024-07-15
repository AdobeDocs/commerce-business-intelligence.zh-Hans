---
title: 载入Adobe Commerce Intelligence
description: 了解Adobe Commerce Intelligence入门。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 载入[!DNL Adobe Commerce Intelligence]

与`store`和`database`设置相关的载入问题可确保您正确设置报表。 有了这些答案，Adobe将针对您商店的设置提供量身定制的报表。

## 商店设置

- *您的商店是否接受访客签出？* — 如果允许客户在注册帐户之前从您的商店购买产品，请选择&#x200B;**是**。

- `Timezone` — 选择您希望在其中查看报告的`timezone`。

- `Currency` — 选择您的商店运营所在的`currency`。

- `Your week starts on...` — 在报表中选择您希望作为一周开始的一周中的哪一天。

- *您使用哪个版本的Commerce？* — 选择您的商店运营所在的`currency`。

- *您的商店是否位于欧盟？* — 如果您回答`Yes`此问题，Adobe将您的Data Warehouse和所有数据托管在欧盟，以符合GDPR。

## 数据库设置

- `Database name` - Commerce事务型数据所在的[!DNL MySQL]数据库&#x200B;*的*&#x200B;名称是什么？

- `Table prefix (optional)` - Commerce数据库中包含的表是否带有任何前缀（例如，`store_`）？ 通常不会出现这种情况，但可以进行自定义。
