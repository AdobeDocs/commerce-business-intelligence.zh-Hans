---
title: 预期Salesforce数据
description: 了解Salesforce数据中支持和不受支持的对象。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 预期 [!DNL Salesforce] 数据

[在 [!DNL Salesforce] 设置完成](../integrations/salesforce.md)，每个可查询项的表 [对象](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)  — 已命名 `sf_/\{sobject-name}`  — 在您的Data warehouse中创建。

>[!NOTE]
>
>每个表的结构（列）取决于对象中包含的字段。

要获取您的组织可用的对象列表，请参阅 [!DNL Salesforce] [获取对象列表文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 拥有对象列表后，请检出 [实体关系图(ERD)部分](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) 之 [!DNL Salesforce] 文档，以了解实体如何相互关联。

## 不支持的对象

目前， [!DNL Salesforce] 当前不会在其API中公开以下对象：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什么是外部对象？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## 相关：

* [正在连接 [!DNL Salesforce]](../integrations/salesforce.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
