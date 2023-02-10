---
title: 报告零售日历
description: 了解如何设置结构以在您的 [!DNL MBI] 帐户。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 零售日历报表

在本文中，我们将演示如何设置结构以使用 [4-5-4零售日历](https://nrf.com/resources/4-5-4-calendar) 在 [!DNL MBI] 帐户。 可视化报表生成器提供了极其灵活的时间范围、间隔和独立设置。 我们的团队还能够帮助您更改一周中的第一天，以符合您的业务偏好。 但是，所有这些设置都适用于传统的月度日历。

由于我们的许多客户会更改其日历以使用零售或会计日期，因此以下步骤将说明如何使用您的数据以及如何使用零售日期创建报表。 尽管以下说明将引用4-5-4零售日历，但您可以根据您的团队使用的任何特定日历（无论是财务日历还是仅是自定义时间范围）更改这些日历。

开始之前，您需要熟悉 [文件加载器](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 并确保你把 `.csv` 以便日期涵盖所有历史数据，并将日期推送到未来。

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入门

您可以 [下载](../../assets/454-calendar.csv) a `.csv` 零售年度4-5-4零售日历版本（2014至2017年）。 请注意，您可能需要根据内部零售日历调整此文件，并延长日期范围以支持您的历史和当前时间范围。 下载文件后，使用File Uploader在 [!DNL MBI] data warehouse。 如果您使用的是4-5-4零售日历的未更改版本，请确保此表中字段的结构和数据类型与以下内容相匹配：

| 列名称 | 列数据类型 | 主键 |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最多255个字符） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style=&quot;table-layout:auto&quot;}

## 要创建的列

* **sales\_order** 表
   * `INPUT` `created\_at` (yyyy-mm-dd 00):00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **零售日历** 文件上传表
   * **当前日期**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL数据类型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >的 `now()` 上述函数专用于PostgreSQL。 尽管 [!DNL MBI] data warehouse在PostgreSQL上托管，有些在Redshift上托管。 如果上述计算返回错误，则可能需要使用Redshift函数 `getdate()` 而不是 `now()`.
   * **当前零售年份** （必须由支持分析师创建）
      * [!UICONTROL Column type]:E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **是否包含在当前零售年度？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL数据类型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **是否包含在上一零售年度？ （是/否）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL数据类型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** 表
   * **已创建\_at（零售年）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 选择 [!UICONTROL table]: `Retail Calendar`
      * 选择 [!UICONTROL column]: `Year Retail`
   * **已创建\_at（零售周）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]:sales\_order。\[INPUT\]已创建\_at(yyyy-mm-dd 00:00:00
         * [!UICONTROL One]:Retail Calendar.Date Retaid
      * 选择 [!UICONTROL table]: `Retail Calendar`
      * 选择 [!UICONTROL column]: `Week Retail`
   * **已创建\_at（零售月）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * 选择 [!UICONTROL table]: `Retail Calendar`
      * 选择 [!UICONTROL column]: `Month Number Retail`
   * **是否包括在上一零售年度？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 选择 [!UICONTROL table]: `Retail Calendar`
      * 选择 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **是否包括在当前零售年度？ （是/否）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * 路径 — 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]:零售 `Calendar.Date Retail`
      * 选择 [!UICONTROL table]: `Retail Calendar`
      * 选择 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 量度

注意：此分析不需要任何新量度。 但是，请确保 [将您在sales\_order表中构建的新列添加为维度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 的所有量度。

## 报表

* **每周订单 — 零售日历(YoY)**
   * 量度 `A`: `2017`
      * [!UICONTROL Metric]:订单数
      * [!UICONTROL Filter]:
         * Created\_at（零售年）= 2017
   * 量度 `B`: `2016`
      * [!UICONTROL Metric]:订单数
      * [!UICONTROL Filter]:
         * Created\_at（零售年）= 2016
   * 量度 `C`: `2015`
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

* **零售日历概述（当前按月零售）**
   * 量度 `A`: `Revenue`
      * 
         [!UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`: `Avg order value`
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

* **零售日历概述（上一零售年份，按月）**
   * 量度 `A`: `Revenue`
      * 
         [!UICONTROL量度]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `B`: `Orders`
      * [!UICONTROL Metric]:订单数
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * 量度 `C`: `Avg order value`
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

上面介绍了如何配置零售日历以与基于 `sales\_order` 表格(例如，`Revenue` 和 `Orders`)，但您也可以扩展此日历以支持任何表上构建的量度的零售日历。 唯一的要求是此表具有有效的日期时间字段，可用于连接到“零售日历”表。

例如，要查看零售日历上的客户级别量度4-5-4，请新建一个 `Same Table` 在 `customer\_entity` 表格，类似于 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 如上所述。 然后，您可以使用此列重现 `One to Many` JOINED\_COLUMN计算(如 `Created_at (retail year)` 和 `Include in previous retail year? (Yes/No)` 加入 `customer\_entity` 表格 `Retail Calendar` 表。

别忘了 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。
