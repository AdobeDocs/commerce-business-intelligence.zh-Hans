---
title: 预期的Google Analytics数据
description: 了解如何与您的Google Analytics量度交互。
exl-id: db9fdaaa-47a9-4095-b1f8-9b6c74c25b7c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 预期[!DNL Google Analytics]数据

在连接[!DNL Google Analytics]集成后，您可以在&#x200B;`Visual Report Builder`*中立即与[!DNL Google Analytics]量度*&#x200B;进行交互。 输入`Visual Report Builder`时，如果单击&#x200B;**[!UICONTROL Add a Metric]**，则[!DNL Google Analytics]配置文件中的一系列指标将显示在Data Warehouse中指标正下方的下拉菜单中。

[!DNL Google Analytics]集成是&#x200B;*实时* — 这意味着当您向报表添加量度时，`Report Builder`会立即从[!DNL Google Analytics] **&#x200B;请求数据。 它还意味着您可以访问的量度的定义方式与在[!DNL Google Analytics]中的定义方式完全相同，并且这些值不是在[!DNL Commerce Intelligence]帐户中的&#x200B;*仓库*，而是仅以可视方式显示在报表中。

+++支持的指标和Dimension(Google Analytics3或Universal Analytics)

>[!NOTE]
>
>2023年7月1日，标准Universal Analytics ([!DNL Google Analytics] 3)属性将不再处理数据。 在2023年7月1日之后，您将能够看到您的Universal Analytics报表。 但是，新数据将只流入[!DNL Google Analytics] 4个属性。

[!DNL Commerce Intelligence]中的[!DNL Google Analytics]集成使用[!DNL Google Analytics] [核心报表API](https://developers.google.com/analytics/devguides/reporting/core/v3/)，并支持以下量度和维度。

>[!NOTE]
>
>为避免出现意外或无意义的结果，请确认您使用的任何维度与`Report Builder`中使用的一个或多个量度兼容。 您可以在[此处](https://ga-dev-tools.google/dimensions-metrics-explorer/)查看。

## 支持的指标

| [!DNL Commerce Intelligence]显示名称 | [!DNL Google Analytics]名称/公式 |
| --- | --- |
| `Page Views` | `ga:pageviews` |
| `Total Time Spent On Page` | `ga:timeOnPage` |
| `Bounces (One Page Visits)` | `ga:bounces` |
| `Entrances` | `ga:entrances` |
| `Exits` | `ga:exits` |
| `Unique Pageviews` | `ga:uniquePageviews` |
| `Ad Clicks` | `ga:adClicks` |
| `Ad Cost` | `ga:adCost` |
| `Cost per Click (CPC)` | `ga:CPC` |
| `Cost per Thousand Impressions (CPM)` | `ga:CPM` |
| `Click-Through Rate (CTR)` | `ga:CTR` |
| `Impressions` | `ga:impressions` |
| `Product Revenue` | `ga:itemRevenue` |
| `Products Purchased` | `ga:itemQuantity` |
| `Revenue` | `ga:transactionRevenue` |
| `Transactions` | `ga:transactions` |
| `Shipping Revenue` | `ga:transactionShipping` |
| `Tax Revenue` | `ga:transactionTax` |
| `Unique Purchases` | `ga:uniquePurchases` |
| `Pageviews After Internal Search` | `ga:searchDepth` |
| `Visit Duration After Internal Search` | `ga:searchDuration` |
| `Exits After Internal Search` | `ga:searchExits` |
| `Internal Search Refinements` | `ga:searchRefinements` |
| `Unique Users Using Internal Search` | `ga:searchUniques` |
| `Bounce Rate` | `ga:visitBounceRate` |
| `Average Time on Page` | `ga:avgTimeOnPage` |
| `Average Session Length` | `ga:avgSessionDuration` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Events` | `ga:totalEvents` |
| `Unique Events` | `ga:uniqueEvents` |
| `Event Value` | `ga:eventValue` |
| `Average Domain Lookup Time` | `ga:avgDomainLookupTime` |
| `Average Page Download Time` | `ga:avgPageDownloadTime` |
| `Average Page Load Time` | `ga:avgPageLoadTime` |
| `Transactions Per Visit` | `ga:transactionsPerVisit` |
| `Sessions` | `ga:sessions` |
| `Users` | `ga:users` |
| `New Users | ga:newUsers` |
| `Sessions Where Internal Search Used` | `ga:searchSessions` |
| `Goal X Starts` | `ga:goal...Starts` |
| `Goal X Completions` | `ga:goal...Completions` |
| `Goal X Conversion Rate` | `ga:goal...ConversionRate` |
| `Goal X Total Value` | `ga:goal...Value` |
| `All Goal Starts` | `ga:goalStartsAll` |
| `All Goal Completions` | `ga:goalCompletionsAll` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Goal Value` | `ga:goal1ValueAll` |

{style="table-layout:auto"}

## 支持的Dimension

| [!DNL Commerce Intelligence]显示名称 | [!DNL Google Analytics]名称/公式 | 可分组？ |
| --- | --- | --- |
| `Ad Content` | `ga:adContent` | `Yes` |
| `Ad Group` | `ga:adGroup` | `Yes` |
| `Matched Search Query` | `ga:adMatchedQuery` | `Yes` |
| `Placement Domain` | `ga:adPlacementDomain` | `Yes` |
| `Placement URL` | `ga:adPlacementUrl` | `Yes` |
| `Affiliation` | `ga:affiliation` | `Yes` |
| `Browser` | `ga:browser` | `Yes` |
| `Browser Version` | `ga:browserVersion` | `Yes` |
| `Campaign` | `ga:campaign` | `Yes` |
| `Continent` | `ga:continent` | `Yes` |
| `Custom Variable 2` | `ga:customVarValue2` | `Yes` |
| `Custom Variable 3` | `ga:customVarValue3` | `Yes` |
| `Custom Variable 5` | `ga:customVarValue5` | `Yes` |
| `Date` | `ga:date` | `No` |
| `Day` | `ga:day` | `No` |
| `Days Since Last Session` | `ga:daysSinceLastSession` | `Yes` |
| `Days Since Referring Campagin` | `ga:daysToTransaction` | `Yes` |
| `Device Category` | `ga:deviceCategory` | `Yes` |
| `Custom Dimension 10` | `ga:dimension10` | `Yes` |
| `Custom Dimension 12` | `ga:dimension12` | `Yes` |
| `Custom Dimension 13` | `ga:dimension13` | `Yes` |
| `Custom Dimension 18` | `ga:dimension18` | `Yes` |
| `Custom Dimension 2` | `ga:dimension2` | `Yes` |
| `Custom Dimension 20` | `ga:dimension20` | `Yes` |
| `Custom Dimension 3` | `ga:dimension3` | `Yes` |
| `Custom Dimension 4` | `ga:dimension4` | `Yes` |
| `Custom Dimension 5` | `ga:dimension5` | `Yes` |
| `Custom Dimension 8` | `ga:dimension8` | `Yes` |
| `Custom Dimension 9` | `ga:dimension9` | `Yes` |
| `Event Action` | `ga:eventAction` | `Yes` |
| `Event Category` | `ga:eventCategory` | `Yes` |
| `Event Label` | `ga:eventLabel` | `Yes` |
| `Exit Page Path` | `ga:exitPagePath` | `Yes` |
| `Flash Version Supported` | `ga:flashVersion` | `Yes` |
| `Hour` | `ga:hour` | `No` |
| `In-Market Segment` | `ga:interestInMarketCategory` | `Yes` |
| `Language` | `ga:language` | `Yes` |
| `Longitude` | `ga:longitude` | `No` |
| `Medium` | `ga:medium` | `Yes` |
| `Metro` | `ga:metro` | `Yes` |
| `Mobile Device Branding` | `ga:mobileDeviceBranding` | `Yes` |
| `Mobile Device Info` | `ga:mobileDeviceInfo` | `Yes` |
| `Month` | `ga:month` | `No` |
| `Operating System` | `ga:operatingSystem` | `Yes` |
| `Operating System Version` | `ga:operatingSystemVersion` | `Yes` |
| `Pages Viewed per Session` | `ga:pageDepth` | `Yes` |
| `Page Path` | `ga:pagePath` | `Yes` |
| `Product Category` | `ga:productCategory` | `Yes` |
| `Product Name` | `ga:productName` | `Yes` |
| `Referral URL` | `ga:referralPath` | `No` |
| `Region (State)` | `ga:region` | `Yes` |
| `Screen Colors` | `ga:screenColors` | `Yes` |
| `Screen Resolution` | `ga:screenResolution` | `Yes` |
| `Internal Search Category` | `ga:searchCategory` | `Yes` |
| `Internal Search Refined Keyword(s)` | `ga:searchKeywordRefinement` | `Yes` |
| `Internal Search Used?` | `ga:searchUsed` | `Yes` |
| `Second Page Path` | `ga:secondPagePath` | `Yes` |
| `Source` | `ga:source` | `Yes` |
| `Sub-Continent` | `ga:subContinent` | `Yes` |
| `Transaction ID` | `ga:transactionId` | `Yes` |
| `Custom (User Defined) Value` | `ga:userDefinedValue` | `Yes` |
| `Year` | `ga:year` | `No` |

{style="table-layout:auto"}

+++

+++支持的指标和Dimension(Google Analytics4)

[!DNL Commerce Intelligence]中的[!DNL Google Analytics]集成使用[!DNL Google Analytics] [数据API v1 (GA4)](https://developers.google.com/analytics/devguides/reporting/data/v1)。

>[!NOTE]
>
> Commerce Intelligence不支持以下维度： `cohort`、`cohortNthDay`、`cohortNthMonth`和`cohortNthWeek`。
>
>为避免出现意外或无意义的结果，请确认您使用的任何维度与`Visual Report Builder`中使用的一个或多个量度兼容。 您可以检查[GA4Dimension和量度资源管理器](https://ga-dev-tools.google/ga4/dimensions-metrics-explorer/)。

+++
