---
title: 载入Adobe Commerce Intelligence
description: 了解如何载入Adobe Commerce Intelligence。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 入门 [!DNL Adobe Commerce Intelligence]

与相关的入门培训问题 `store` 和 `database` 设置可确保您正确设置报表。 有了这些答案，Adobe将针对您商店的设置提供量身定制的报表。

## 商店设置

- *您的商店是否接受访客结帐？*  — 选择 **是** 如果您允许客户在不注册帐户的情况下从您的商店购买商品。

- `Timezone`  — 选择 `timezone` 您希望在中查看您的报表。

- `Currency`  — 选择 `currency` 你的商店经营的那个。

- `Your week starts on...`  — 在报表中，选择要作为一周开始的一周中的哪一天。

- *您使用哪个版本的Commerce？*  — 选择 `currency` 你的商店经营的那个。

- *你的店在欧盟吗？*  — 如果您回答 `Yes` 对于此问题，Adobe会根据GDPR将您的Data Warehouse和所有数据托管在欧盟。

## 数据库设置

- `Database name`  — 什么是 *的名称 [!DNL MySQL] 数据库* Commerce事务数据驻留在何处？

- `Table prefix (optional)`  — 您的Commerce数据库中包含的表是否前面有任何内容(例如， `store_`)？ 通常不会出现这种情况，但可以进行自定义。
