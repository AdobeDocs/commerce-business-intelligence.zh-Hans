---
title: 导入其他广告支出数据
description: 了解如何将离线或其他广告支出数据导入 [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 导入其他广告支出数据

上传广告支出数据将允许您将广告成本与客户结合起来衡量活动ROI `lifetime value (CLV)` 从您的营销活动获得的用户数量。

## 上传广告成本数据

分析广告支出数据的第一步是获取数据。 由于大多数广告平台都允许您导出报表，因此我们建议您从广告平台导出原始数据，并将其直接上传到 [!DNL MBI] 没有任何操纵。 您可以对data warehouse中的数据执行操作，因此无需加倍努力。

导出广告支出数据后，请使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 将数据导入data warehouse。 您可以将新数据上传到同一 [!DNL MBI] 表格。

## 离线源

除了在线营销活动外，您还可能有离线广告，例如在收音机或广告牌上。 要考虑这些情况，您可以手动将包含成本数据的电子表格上传到 [!DNL MBI].

在创建 `.csv` 文件来记录广告支出数据。 模板文件也附在本文底部，以作为示例。 推荐的列包括：

* `ID`  — 这是数据库用作主键的每个数据行的唯一标识符。 每行的值必须不同。
* `Date`  — 这是营销活动运行的日期，格式为yyyy-mm-dd。
* `Amount`  — 这是您在营销活动上花费的金额。
* `campaign`  — 这是营销活动名称。 如果您使用 [!DNL Google Analytics] 要跟踪您的其他广告支出数据，它应与utm\_campaign名称匹配。
* `source`  — 这是源名称。 如果您使用 [!DNL Google Analytics]，此值应与 `utm_source` 名称。
* `other` （可选） — 您还可以加入其他列，以帮助您细分促销活动和成本。 此外，还可以将多个不同的UTM营销活动名称汇总为单个一致的营销活动，以便进行跟踪。 使用V-Lookup查找第二个工作表，将每个促销活动名称与其他名称匹配并在此处动态报告，而不是手动设置。

## 相关

* [连接 [!DNL AdWords] 数据](../integrations/google-adwords.md)
* [提高广告活动的ROI](../../analysis/roi-ad-camp.md)
