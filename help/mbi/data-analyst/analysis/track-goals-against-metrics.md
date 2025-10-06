---
title: 根据量度跟踪目标
description: 了解如何设置仪表板，以帮助您根据实际数据（包括收入、新注册用户和一段时间内的订单）跟踪业务目标。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 根据绩效指标跟踪目标

大多数客户希望跟踪其&#x200B;**业务目标**，但未意识到这在[!DNL Adobe Commerce Intelligence]中是可能的。 本主题将演示如何设置一个功能板，帮助您根据实际数据（包括收入、新注册用户和一段时间内的订单）跟踪业务目标。 您还将了解如何比较各年的业绩，所有这些都在功能板中，如下所示：

![显示目标跟踪实际量度绩效的功能板](../../assets/Goals-_dashboard_2.png)

在开始之前，您应该查看[文件上载程序](../importing-data/connecting-data/using-file-uploader.md)，并确保已定义了给定时间段的业务目标。

## 快速入门

您需要首先上传一个文件，其中包含贵企业的特定每日/每月/每季度目标。

您可以使用[文件上载程序](../importing-data/connecting-data/using-file-uploader.md)以及下面的图像来格式化文件。 客户端在[!DNL Commerce Intelligence]中跟踪的最常见目标包括订单、收入和新注册帐户。

用于跟踪目标和量度的![Excel电子表格模板](../../assets/Goals-_Excel.png)

## 量度

为每个目标创建一个新量度。 例如，如果您上传每月收入和订单目标，则需要创建两个新量度：

* **每月收入目标**
* 在&#x200B;**`Monthly goals`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`Revenue target`**&#x200B;列上
* 按&#x200B;**`Month`**&#x200B;时间戳排序

* **每月订单目标**
* 在&#x200B;**`Monthly goals`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`Orders target`**&#x200B;列上
* 按&#x200B;**`Month`**&#x200B;时间戳排序

* **每月新注册的帐户目标**
* 在&#x200B;**`Monthly goals`**&#x200B;表中
* 此量度执行&#x200B;**总和**
* 在&#x200B;**`New registered accounts target`**&#x200B;列上
* 按&#x200B;**`Month`**&#x200B;时间戳排序

## 报告

在分析目标时，将静态值和可视化图表混合使用会很有帮助。 以下是三个示例报表，可帮助您开始跟踪收入表现。

* 剩余&#x200B;**收入以实现目标**
* 量度`A`： `Revenue`
* &#x200B;
  [!UICONTROL 量度]: `Revenue`

* 量度`B`： `Target Revenue`
* [!UICONTROL Metric]： `Monthly Revenue Target`

* [!UICONTROL Formula]： `Revenue left to achieve target`
* &#x200B;
  [!UICONTROL 公式]: `(B-A)`
* &#x200B;
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]：（无论您需要什么相关时间段）
* &#x200B;
  [!UICONTROL Interval]: `Month`
* &#x200B;
  [!UICONTROL 图表类型]: `Scalar`

* **收入目标**
* 量度`A`： `Revenue`
* &#x200B;
  [!UICONTROL 量度]: `Revenue`

* 量度`B`： `Target Revenue`
* [!UICONTROL Metric]： `Monthly Revenue Target`

* 量度`C`： `Revenue (amount change since previous year)` （隐藏）
* &#x200B;
  [!UICONTROL 量度]: `Revenue`
* [!UICONTROL Perspective]： `Amount change vs. Previous year`

* [!UICONTROL Formula]：（去年这个月）
* &#x200B;
  [!UICONTROL 公式]: `(A-C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

* 关闭`Multiple Y-Axes`
* [!UICONTROL Time period]：（无论您需要什么相关时间段）*
* &#x200B;
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]： `Line Chart`

完成上述收入目标报表后，您可以针对订单、注册帐户或已包括在目标文件上传中的任何其他值，创建相同的目标报表。

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于此页面顶部的图像。
