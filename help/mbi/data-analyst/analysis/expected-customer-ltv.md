---
title: Pro的预期生命周期值(LTV)分析
description: 了解如何设置功能板，以帮助您了解客户的存留期价值增长和客户的预期存留期价值。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 预期生命周期值分析

本文演示了如何设置功能板，以帮助您了解客户存留期价值的增长以及客户的预期存留期价值。

![](../../assets/exp-lifetim-value-anyalysis.png)

此分析仅适用于采用新架构的Pro客户。 如果您的帐户有权访问 `Persistent Views` 下的功能 `Manage Data` 侧栏中，您位于新架构上，可以按照此处列出的说明自行构建此分析。

在开始之前，您需要先熟悉 [同类群组report builder。](../dev-reports/cohort-rpt-bldr.md)

## 计算列

要在上创建的列 **订单** 表（如果使用） **30天月**：

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **定义：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* 定义： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

要在上创建的列 **`orders`** 表（如果使用） **日历** 月：

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* 定义： `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **定义：**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* 定义： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 量度

### 量度说明

要创建的量度

* **按第一订单日期划分的不同客户**
   * 如果启用来宾订单，请使用 `customer_email`

* 在 **`orders`** 表
* 此量度执行 **对非重复值计数**
* 在 **`customer_id`** 列
* 排序依据 **`Customer's first order date`** 时间戳

>[!NOTE]
>
>确保 [将所有新列作为维度添加到量度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。

## 报告

### 报告说明

**按月份每个客户的预期收入**

* 量度 `A`： `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （为X选择一些合理的数字，例如24个月）
   * `Is in current month?` = `No`

* 
   [！UICONTROL量度]: `Revenue`
* [!UICONTROL Filter]:

* 量度 `B`： `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 量度 `C`： `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

其他图表详细信息

* [!UICONTROL Time period]: `All time`
* 时间间隔： `None`
* [!UICONTROL Group by]： `Calendar months between first order and this order`  — 全部显示
* 更改 `group by` 对于 `All time customers` 使用“量度”旁边的“铅笔”图标可将“量度”转换为“独立” `group by`
* 编辑 `Show top/bottom` 字段如下所示：
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**按同类群组划分的每月平均收入**

* 量度 `A`： `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**按同类群组显示的每月累计平均收入**

* 量度 `A`： `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能与页面顶部的图像类似。

如果您在构建此分析时遇到任何问题，或者只是想让专业服务团队参与进来， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
