---
title: Pro的预期生命周期值(LTV)分析
description: 了解如何设置功能板，以帮助您了解客户生命周期价值增长和客户预期生命周期价值。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 预期生命周期值分析

在本文中，我们将演示如何设置功能板，以帮助您了解客户生命周期价值的增长和客户的预期生命周期价值。

![](../../assets/exp-lifetim-value-anyalysis.png)

此分析仅适用于新架构的专业客户。 如果您的帐户有权访问 `Persistent Views` 功能 `Manage Data` 侧栏中，您使用的是新架构，可以按照此处列出的说明自行构建此分析。

在开始之前，您需要熟悉我们的 [同类群组报表生成器。](../dev-reports/cohort-rpt-bldr.md)

## 计算列

要在 **订购** 表 **30天月**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **定义：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* 定义： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

要在 **`orders`** 表 **日历** 月：

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
* [!UICONTROL Column input]:A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* 定义： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 量度

### 量度说明

要创建的量度

* **按首次订购日期划分的不同客户**
   * 如果启用来宾订单，请使用 `customer_email`

* 在 **`orders`** 表
* 此量度执行 **计算非重复值**
* 在 **`customer_id`** 列
* 由 **`Customer's first order date`** timestamp

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

### 报告说明

**按月预计每位客户收入**

* 量度 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （为X选取一些合理的数字，例如24个月）
   * `Is in current month?` = `No`

* 
   [!UICONTROL量度]: `Revenue`
* [!UICONTROL Filter]:

* 量度 `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 量度 `C`: `All time customers by month since first order (hide)`
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
* [!UICONTROL Group by]: `Calendar months between first order and this order`  — 显示全部
* 更改 `group by` 对于 `All time customers` 使用 `group by`
* 编辑 `Show top/bottom` 字段如下所示：
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**按同类群组划分的每月平均收入**

* 量度 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**按同类群组划分的每月累积平均收入**

* 量度 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与页面顶部的图像类似。

如果您在构建此分析时遇到任何问题，或者只想与我们的专业服务团队接洽， [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
