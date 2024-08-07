---
title: 导入其他广告支出数据
description: 了解如何将离线或其他广告支出数据导入 [!DNL Commerce Intelligence]。
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 导入其他广告支出数据

通过上传广告支出数据，您可以将广告成本与从营销活动中获取的`customer lifetime value (CLV)`个用户相结合，从而衡量营销活动ROI。

## 上传广告成本数据

分析广告支出数据的第一步是获取数据。 由于大多数广告平台都允许您导出报表，因此Adobe建议您从广告平台导出原始数据并直接将其上传到[!DNL Commerce Intelligence]，而无需进行任何操作。 您可以对Data Warehouse中的数据执行操作，因此无需加倍努力。

导出广告支出数据后，使用[`File Upload`功能](../connecting-data/using-file-uploader.md)将数据导入Data Warehouse。 您可以在一段时间内将新数据上传到同一[!DNL Commerce Intelligence]表。

## 脱机源

除了在线促销活动之外，您还可能会有离线广告，例如在收音机或广告牌上。 要考虑这些情况，您可以手动将带有成本数据的电子表格上传到[!DNL Commerce Intelligence]。

创建`.csv`文件以记录广告支出数据时，建议使用下面探讨的表结构。 作为示例，还将在本主题底部附加一个模板文件。 建议的列包括：

* `ID` — 这是数据库用作主键的每个数据行的唯一标识符。 每一行的此项必须不同。
* `Date` — 这是营销活动运行的日期，格式为yyyy-mm-dd。
* `Amount` — 这是您在营销活动上花费的金额。
* `campaign` — 这是营销活动名称。 如果您使用[!DNL Google Analytics]跟踪您的其他广告支出数据，它应该与utm\_campaign名称匹配。
* `source` — 这是源名称。 如果您使用的是[!DNL Google Analytics]，此名称应与`utm_source`名称匹配。
* `other`（可选） — 您还可以合并其他列，以帮助您划分促销活动和成本。 它还可以作为一种方法，将多个不同的UTM营销活动名称汇总到单个一致的营销活动中以进行跟踪。 最好不要手动进行此设置，而是将V-Lookup用于第二个工作表以将每个促销活动名称与其他名称进行匹配，并在此处动态报告该名称。

## 相关

* [连接 [!DNL AdWords] 数据](../integrations/google-adwords.md)
* [提高广告促销活动的ROI](../../analysis/roi-ad-camp.md)
