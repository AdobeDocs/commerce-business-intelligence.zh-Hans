---
title: 在零售日历上报告
description: 了解如何设置结构以在您的网站中使用4-5-4零售日历 [!DNL Commerce Intelligence] 帐户。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 在零售业日历中报告

本主题演示了如何设置结构以使用 [4-5-4零售日历](https://nrf.com/resources/4-5-4-calendar) 在您的 [!DNL Adobe Commerce Intelligence] 帐户。 可视化Report Builder提供了极其灵活的时间范围、间隔和独立的设置。 但是，所有这些设置都适用于传统的每月日历。

由于许多客户更改其日历以使用零售日期或会计日期，因此以下步骤说明了如何使用您的数据以及使用零售日期创建报表。 尽管下面的说明引用了4-5-4零售日历，但您可以为您的团队使用的任何特定日历更改它们，无论是财务日历还是自定义时间范围。

在开始之前，您应该查阅 [文件上传程序](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 并确保您已将 `.csv` 文件。 这可确保日期涵盖所有历史数据并将日期推送到未来。

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

您可以 [下载](../../assets/454-calendar.csv) a `.csv` 2014年至2017年零售年度的4-5-4零售日历版本。 您可能需要根据内部零售日历调整此文件，并扩展日期范围以支持您的历史和当前时间范围。 下载文件后，使用文件上传程序在 [!DNL Commerce Intelligence] data warehouse。 如果您使用的是4-5-4零售日历的未更改版本，请确保此表字段的结构和数据类型与以下内容匹配：

| 列名称 | 列数据类型 | 主键 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最多255个字符） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 要创建的列

* **sales\_order** 表
   * `INPUT` `created\_at` (yyyy-mm-dd 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **零售日历** 文件上载表
   * **当前日期**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [！UICONTROL数据类型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >此 `now()` 上述函数特定于PostgreSQL。 尽管最多 [!DNL Commerce Intelligence] data warehouse托管在PostgreSQL上，某些应用程序可能托管在Redshift上。 如果上述计算返回错误，您可能需要使用Redshift函数 `getdate()` 而不是 `now()`.
   * **当前零售年份** （必须由支持分析人员创建）
      * [!UICONTROL Column type]：E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **是否包括在当前零售年度？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [！UICONTROL数据类型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **是否包含在以前的零售年度中？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [！UICONTROL数据类型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** 表
   * **创建时间\_at（零售年份）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 选择 [!UICONTROL table]： `Retail Calendar`
      * 选择 [!UICONTROL column]： `Year Retail`
   * **创建时间\_at（零售周）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]： sales\_order。\[INPUT\]已创建\_at (yyyy-mm-dd 00):00:00
         * [!UICONTROL One]：零售业Calendar.Date零售业
      * 选择 [!UICONTROL table]： `Retail Calendar`
      * 选择 [!UICONTROL column]： `Week Retail`
   * **创建时间\_at（零售月份）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 选择 [!UICONTROL table]： `Retail Calendar`
      * 选择 [!UICONTROL column]： `Month Number Retail`
   * **是否包含在上一个零售年度中？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：零售业 `Calendar.Date Retail`
      * 选择 [!UICONTROL table]： `Retail Calendar`
      * 选择 [!UICONTROL column]： `Include in previous retail year? (Yes/No)`
   * **是否包含在当前零售年度中？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：零售业 `Calendar.Date Retail`
      * 选择 [!UICONTROL table]： `Retail Calendar`
      * 选择 [!UICONTROL column]： `Include in current retail year? (Yes/No)`

## 量度

注意：此分析不需要新指标。 但是，请确保 [将您在sales\_order表中构建的新列添加为维](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ，然后继续查看这些报表。

## 报告

* **每周订单 — 零售日历（按年）**
   * 量度 `A`： `2017`
      * [!UICONTROL Metric]：订单数
      * [!UICONTROL Filter]:
         * 创建时间\_at（零售年份）= 2017
   * 量度 `B`： `2016`
      * [!UICONTROL Metric]：订单数
      * [!UICONTROL Filter]:
         * Created\_at （零售年份）= 2016
   * 量度 `C`： `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * 关闭 `multiple Y-axes`

* **零售日历概述（当前零售年份，按月）**
   * 量度 `A`： `Revenue`
      * 
         [！UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`： `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`： `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **零售业日历概述（上一零售年，按月）**
   * 量度 `A`： `Revenue`
      * 
         [！UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`： `Orders`
      * [!UICONTROL Metric]：订单数
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`： `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## 后续步骤

上文中介绍了如何配置零售日历，使其与基于的任何指标兼容。 `sales\_order` 表格(例如 `Revenue` 或 `Orders`)。 您还可以对其进行扩展，以支持基于任何表构建的量度的零售日历。 唯一要求是此表必须有一个有效的datetime字段，该字段可用于联接到零售业日历表。

例如，要在4-5-4零售日历中查看客户级别指标，请创建 `Same Table` 在中计算 `customer\_entity` 表，类似于 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 如上所述。 然后，您可以使用此列复制 `One to Many` JOINED\_COLUMN计算(如 `Created_at (retail year)`)和 `Include in previous retail year? (Yes/No)` 加入 `customer\_entity` 表 `Retail Calendar` 表格。

别忘了 [将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。
