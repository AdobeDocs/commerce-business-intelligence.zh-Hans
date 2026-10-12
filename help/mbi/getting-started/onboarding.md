---
title: 载入Adobe Commerce Intelligence
description: 了解Adobe Commerce Intelligence入门。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: 'https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
    internal-label: GDPR
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%
---
# 载入[!DNL Adobe Commerce Intelligence]

与`store`和`database`设置相关的载入问题可确保您正确设置报表。 有了这些答案，Adobe将针对您商店的设置提供量身定制的报表。

## 商店设置

- *您的商店是否接受访客签出？*  — 如果允许客户在注册帐户之前从您的商店购买商品，请选择&#x200B;**是**。

- `Timezone` — 选择您希望在其中查看报告的`timezone`。

- `Currency` — 选择您的商店运营所在的`currency`。

- `Your week starts on...` — 在报表中选择您希望作为一周开始的一周中的哪一天。

- *您使用哪个版本的Commerce？*  — 选择您的商店运营所在的`currency`。

- *您的商店是否位于欧盟？*  — 如果您回答`Yes`此问题，Adobe将根据GDPR将您的Data Warehouse和所有数据托管在欧盟。

## 数据库设置

- `Database name` - Commerce事务型数据所在的[!DNL MySQL]数据库&#x200B;*的*&#x200B;名称是什么？

- `Table prefix (optional)` - Commerce数据库中包含的表是否带有任何前缀（例如，`store_`）？ 通常不会出现这种情况，但可以进行自定义。
