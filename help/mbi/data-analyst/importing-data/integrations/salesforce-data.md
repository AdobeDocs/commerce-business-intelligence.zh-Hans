---
title: 預期Salesforce資料
description: 瞭解Salesforce資料中支援和不支援的物件。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 預期 [!DNL Salesforce] 資料

晚於 [[!DNL Salesforce] 設定](../integrations/salesforce.md) 完整，每個可查詢專案都有一個表格 [物件](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)  — 已命名 `sf_/\{sobject-name}`  — 在您的Data Warehouse中建立。

>[!NOTE]
>
>每個表格的結構（欄）取決於物件中包含的欄位。

若要取得貴組織可用的物件清單，請參閱 [!DNL Salesforce] [取得物件清單檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). 擁有物件清單後，請出庫 [實體關係圖(ERD)區段](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) 之 [!DNL Salesforce] 說明檔案以瞭解實體如何相互關聯。

## 不支援的物件

目前， [!DNL Salesforce] 目前不會在其API中公開下列物件：

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [什麼是外部物件？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

## 相關：

* [正在連線 [!DNL Salesforce]](../integrations/salesforce.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
