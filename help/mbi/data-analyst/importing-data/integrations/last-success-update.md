---
title: 了解数据库和SQL编辑器之间的结果
description: 了解数据库和SQL编辑器之间的结果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
ht-degree: 0%

---

# 数据库结果与[!DNL SQL Editor]个结果

您可能很想知道您的`Last successful update began`页面中的`Integrations`字段是什么：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 了解`timestamp`字段

它显示帐户上`timestamp`最后成功更新周期&#x200B;_的开始_（在帐户中设置的时区）。

- 如果任何同步的表在上次更新周期中遇到问题，则此时间戳为&#x200B;*未更新*。
- 因此，可能会出现使用新数据更新报告的情况，但&#x200B;*上次成功更新开始*&#x200B;仍然滞后。

## 识别“真正的”最后一个数据点

特定集成的最新数据点由每个集成右侧的`Last Data Point Received`时间戳确定。 该时间戳是指您的Data Warehouse上次成功从该源接收数据点的时间，无论该源是数据库、API还是第三方集成。

为了检查来自&#x200B;*特定表*&#x200B;的数据的刷新情况，Adobe建议创建一个快速的[[!DNL SQL] 报告](../../dev-reports/sql-rpt-bldr.md)，对您帐户上最重要的表执行`MAX(timestamp)`。 将此时间戳与`Last Data Point`进行比较可指示该问题影响整个帐户还是表的子集。 Adobe建议对三到四个常用重要表执行此操作。

- 如果`MAX(timestamp)`值比`Last Data Point Received`更新，则意味着表的子集受到影响，但整个帐户的更新周期是稳定的。
- 如果`MAX(timestamp)`值等于或早于`Last Data Point Received`，则意味着帐户的更新周期受到影响。 在这种情况下，[提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
