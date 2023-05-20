---
title: 预期的 Salesforce 数据
description: 了解 Salesforce 数据中支持和不支持的对象。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 预期 [!DNL Salesforce] 数据

[[!DNL Salesforce] 设置 ](../integrations/salesforce.md) 完成后，会在您的数据仓库中为每个可查询 [ 对象 ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) 命名 `sf_/\{sobject-name}` 的表创建一个表格。

>[!NOTE]
>
>每个表的结构（列）取决于对象中包含的字段。

要获取贵组织可使用的对象列表，请参阅 [!DNL Salesforce] [ 获取对象文档 ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm) 列表。 列表对象后，请查看 [ 文档的实体关系图（ERD）部分 ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) ，以了解实体之间的关联情况 [!DNL Salesforce] 。

## 不支持的对象

目前， [!DNL Salesforce] 当前不会在其 API 中公开以下对象：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [ 什么是外部对象？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [连接 [!DNL Salesforce]](../integrations/salesforce.md)
* [Reauthenticating 集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
