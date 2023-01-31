---
title: 预期的Salesforce数据
description: 了解Salesforce数据中受支持和不受支持的对象。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 预期 [!DNL Salesforce] 数据

[在 [!DNL Salesforce] 设置完成](../integrations/salesforce.md)，每个查询的表 [对象](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm)  — 已命名 `sf_/\{sobject-name}`  — 将在您的data warehouse中创建。

>[!NOTE]
>
>每个表的结构（列）取决于对象中包含的字段。

要获取组织可用的对象列表，请参阅 [!DNL Salesforce] [获取对象列表文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 在有对象列表后，请检查 [实体关系图(ERD)部分](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_majors.htm) of [!DNL Salesforce] 文档以了解实体如何彼此关联。

## 不支持的对象

此时， [!DNL Salesforce] 当前不在其API中公开以下对象：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什么是外部对象？](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
