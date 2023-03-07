---
title: 根据量度跟踪目标
description: 了解如何设置仪表板，以帮助您根据实际数据（包括收入、新注册用户和一段时间的订单）跟踪业务目标。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 根据绩效指标跟踪目标

大多数客户都希望跟踪其 **业务目标**，但没有意识到这在 [!DNL MBI]. 本文演示如何设置一个仪表板，帮助您根据实际数据（包括收入、新注册用户和一段时间的订单）跟踪业务目标。 您还将了解如何比较各年的业绩，所有这些都在功能板中，如下所示：

![](../../assets/Goals-_dashboard_2.png)

在开始之前，您需要先熟悉 [文件上载程序](../importing-data/connecting-data/using-file-uploader.md) 并确保您定义了给定时期的业务目标。

## 快速入门

您需要首先上传一个文件，其中包含贵企业的特定每日/每月/每季度目标。

您可以使用 [文件上载程序](../importing-data/connecting-data/using-file-uploader.md) 和下图来格式化您的文件。 客户端跟踪的最常见目标 [!DNL MBI] 包括“订单”、“收入”和“新注册帐户”。

![](../../assets/Goals-_Excel.png)

## 量度

为每个目标创建一个新指标。 例如，如果您上传每月收入和订单目标，则需要创建两个新量度：

* **每月收入目标**
* 在 **`Monthly goals`** 表
* 此量度执行 **总和**
* 在 **`Revenue target`** 列
* 排序依据 **`Month`** 时间戳

* **每月订单目标**
* 在 **`Monthly goals`** 表
* 此量度执行 **总和**
* 在 **`Orders target`** 列
* 排序依据 **`Month`** 时间戳

* **每月新注册帐户目标**
* 在 **`Monthly goals`** 表
* 此量度执行 **总和**
* 在 **`New registered accounts target`** 列
* 排序依据 **`Month`** 时间戳

## 报告

与往常一样，在分析目标时，将静态值和可视图表混合使用会很有帮助。 下面是三个示例报表，可帮助您开始跟踪收入表现。

* **剩余收入以实现目标**
* 量度 `A`： `Revenue`
* 

   [！UICONTROL量度]: `Revenue`

* 量度 `B`： `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [！UICONTROL公式]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]：（无论您希望使用什么相关时间段）
* 
   [!UICONTROL Interval]: `Month`
* 

   [！UICONTROL图表类型]: `Scalar`

* **收入目标**
* 量度 `A`： `Revenue`
* 

   [！UICONTROL量度]: `Revenue`

* 量度 `B`： `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 量度 `C`： `Revenue (amount change since previous year)` （隐藏）
* 
   [！UICONTROL量度]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]：（去年这个月）
* 
   [！UICONTROL公式]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* 关闭 `Multiple Y-Axes`
* [!UICONTROL Time period]：（无论您希望使用什么相关时间段）*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

完成上述收入目标报表后，您可以针对订单、注册帐户或已包括在目标文件上传中的任何其他值，创建相同的目标报表。

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于此页面顶部的图像。
