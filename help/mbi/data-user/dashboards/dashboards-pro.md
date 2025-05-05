---
title: 开箱即用的功能板
description: 了解现成的功能板，为您的业务提供洞察信息。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# 现成仪表板

[!DNL Adobe Commerce Intelligence]包含现成的功能板，可提供对业务的洞察信息。 使用功能板，您可以检查基本指标的运行状况，例如用户生命周期收入、重复购买次数、在给定时间段内购买的热门产品等等。 创建这些预配置的功能板是为了帮助您做出明智的业务决策。

>[!NOTE]
>
>对这些仪表板的访问取决于您的帐户类型和访问级别。 如果您没有看到这些仪表板，请联系[支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)。

## 报告可用性

对于`Customers`和`Executive Summary`功能板，某些报告仅根据您商店的签出配置提供。 具体来说，如果您的商店允许访客签出或不允许访客签出。

## 客户（允许访客结帐）

“客户”（允许访客结帐）仪表板提供有关客户群的信息，例如他们的购买行为。 此仪表板可帮助您提高客户维系率并确定哪些客户可带来最高收入。

### 报告

| 名称 | 描述 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 过去30天内从未下过订单的客户的订单。 |
| `Orders by Existing Customers (Past 30 Days)` | 过去30天内至少下过一次订单的客户的订单。 |
| `Total Unique Customers (Past 30 Days)` | 过去30天内下单的唯一客户数。 |
| `Orders by New vs Existing Customers` | 没有先前订单的客户与至少有一个先前订单的客户之间的订单数。 |
| `Subsequent Order Probability (All Time)` | 已下订单的客户再次下订单的可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 已下多张订单的所有客户的百分比。 |
| `Median Time Between Orders (All Time)` | 每位客户在下单与下单之间所花费的中位数。 |
| `Subsequent Order Probability` | 已下订单的客户下另一张订单的可能性，按订单编号细分。 也就是说，按一次订购的客户的百分比，按二次订购的客户的百分比，按二次订购的客户的百分比，按三分之一订购的客户的百分比，依此类推。 |
| `Time Between Orders` | 客户在订单之间花费的平均时间和中间时间，按订单编号细分（即订单一到二、两到三等之间的时间）。 |
| `Number of Customers - Lifetime Orders` | 对于客户存留期内的给定订单数，已下订单的客户数以及该数字代表的整个客户群的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 首次购买且仅在3到6个月前购买的客户。 |
| `Avg LTV by First Order` | 比较各个同类群组的累积平均客户存留期收入。 同类群组由客户首次购买的月份定义。 例如，`Jan 2020`同类群组显示首次购买时间是2020年1月的客户的累积平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比较客户首次购买后30天内的平均收入与其整个生命周期内的收入。 每个气泡对应于一个航运区域，每个气泡的大小表示从该区域获得的客户数。 |

## 客户（不允许访客结帐）

“客户”（不允许来宾结帐）仪表板提供有关客户群的信息，例如他们的购买行为以及从帐户注册到订单投放的转化情况。 此仪表板可帮助您提高客户维系率并确定哪些客户可带来最高收入。

### 报告

| 名称 | 描述 |
|---|---|
| `Account Registration (Past 30 Days)` | 过去30天内在您的商店注册帐户的人数。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 过去30天内在您的商店注册了帐户，并且至少下过一次订单的人数。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 在过去30天内注册的已下订单的帐户百分比。 |
| `% Conversion from Registration to First Order` | 按注册月份列出的已发出订单的注册帐户的百分比。 |
| `Orders by New vs Existing Customers` | 没有先前订单的客户与至少有一个先前订单的客户之间的订单数。 |
| `Subsequent Order Probability (All Time)` | 已下订单的客户再次下订单的可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 已下多张订单的所有客户的百分比。 |
| `Median Time Between Orders (All Time)` | 每位客户在下单与下单之间所花费的中位数。 |
| `Subsequent Order Probability` | 已下订单的客户下达另一个订单的可能性，按订单编号细分。 也就是说，只有一次订购的客户，有二次订购的客户，有二次订购的客户，有二次订购的客户，有三次订购的客户，依此类推。 |
| `Time Between Orders` | 客户在订单之间花费的平均时间和中间时间，按订单编号细分（即订单一到二、两到三等之间的时间）。 |
| `Number of Customers - Lifetime Orders` | 对于客户存留期内的给定订单数，已下订单的客户数以及该数字代表的整个客户群的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 首次购买且仅在3到6个月前购买的客户。 |
| `Avg LTV by First Order` | 比较各个同类群组的累积平均客户存留期收入。 同类群组由客户首次购买的月份定义。 例如，一个2020年1月同类群组显示首次购买时间是2020年1月的客户的累积平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比较客户首次购买后30天内的平均收入与其整个生命周期内的收入。 每个气泡对应于一个航运区域，每个气泡的大小表示从该区域获得的客户数。 |

## 执行摘要（允许访客结帐）

“执行摘要（允许访客结账）”仪表板可以让您简要了解订单和收入方面的业务情况。 此仪表板专为管理人员而设计，旨在全面了解业务绩效，但也可为其他人提供有见地的见解。

### 报告

| 名称 | 描述 |
|---|---|
| `Revenue (Current Month)` | 您的商店在当前月份生成的收入。 在这种情况下，收入被定义为客户在订单上支付的最终价格。 |
| `Revenue (Past 6 Months by Day)` | 总每日收入，与之前七天的平均每日收入重叠。 在这种情况下，收入被定义为客户在订单上支付的最终价格。 |
| `% Change in Revenue (MoM MTD)` | 本月（到目前为止）与上月同一部分的收入比较。 |
| `Revenue from New vs Existing Customers (Current Month)` | 当月（迄今）的收益来自新（首次）客户与现有客户（发出第二次或以上订单）之比较。 |
| `Average Order Value (Current Month)` | 当月（截至目前）所下订单的每日平均值。 订单值定义为客户在订单上支付的最终价格。 |
| `Orders (Current Month)` | 当月（到目前为止）您商店中下达的订单数。 |
| `% Change in Orders (MoM MTD)` | 本月（到目前为止）与上月同一部分的订单数的比较。 |
| `Orders by New Customers (Current Month)` | 以前从未下过订单的客户当月的订单。 |
| `Orders by Existing Customers (Current Month)` | 当月至少下过一次订单的客户的订单。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 本年度内每周按无先前订单的客户与至少有一笔先前订单的客户列出的订单数（到目前为止）。 |

## 执行摘要（不允许来宾结账）

“执行摘要（不允许来宾结帐）”仪表板可以让您简要了解订单、收入和帐户注册方面的业务情况。 此仪表板专为管理人员而设计，旨在全面了解业务绩效，但也可为其他人提供有见地的见解。

### 报告

| 名称 | 描述 |
|---|---|
| `Revenue (Current Month)` | 您的商店本月已生成的收入。 在这种情况下，收入被定义为客户在订单上支付的最终价格。 |
| `Revenue (Past 6 Months by Day)` | 总每日收入，与之前七天的平均每日收入重叠。 在这种情况下，收入被定义为客户在订单上支付的最终价格。 |
| `% Change in Revenue (MoM MTD)` | 本月迄今为止的收入与上月同期的收入比较。 |
| `Revenue from New vs Existing Customers (Current Month)` | 当月（迄今）的收益来自新（首次）客户与现有客户（发出第二次或以上订单）之比较。 |
| `Average Order Value (Current Month)` | 当月（截至目前）所下订单的每日平均值。 订单值定义为客户在订单上支付的最终价格。 |
| `Orders (Current Month)` | 当月（到目前为止）您商店中下达的订单数。 |
| `% Change in Orders (MoM MTD)` | 本月（到目前为止）与上月同一部分的订单数的比较。 |
| `Account Registrations (Current Month)` | 本月截至目前新注册的账户数量。 |
| `% Conversion from Registration to First Order (Current Month)` | 本月迄今为止已注册订购的帐户的百分比。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 截至目前为止，今年每周已注册且已下订单的帐户百分比。 |

## 订购

“订单”控制面板提供有关订单交易量、订单状态、使用的优惠券代码、生成的收入以及使用的付款方法的洞察。 例如，您可以跟踪履行流程，并确保不存在问题或瓶颈事件。

>[!NOTE]
>
>此仪表板上的报告可用于连接到具有任一配置类型（访客签出，无访客签出）的存储区的帐户。

### 报告

| 名称 | 描述 |
|---|---|
| `Orders (Past 30 Days)` | 过去30天内向您的商店下达的订单数。 |
| `Revenue (Past 30 Days)` | 您的商店在过去30天内产生的收入。 收入被定义为客户在订单上支付的最终价格。 |
| `Average Order Value (Past 30 Days)` | 过去30天内发出的订单的平均值。 订单值定义为客户在订单上支付的最终价格。 |
| `Orders` | 每月您商店中的订单数。 |
| `Revenue by Payment Method` | 按支付方式拆分的商店已产生的收入。 收入被定义为客户在订单上支付的最终价格。 |
| `AOV by New vs Existing Customers` | 店内订单的每月平均价值，按无先前订单的客户与至少有一笔先前订单的客户所下的订单进行拆分。 订单值定义为客户在订单上支付的最终价格。 |
| `% Orders by Status (Past 30 Days)` | 过去30天内每天当前处于每种订单状态的订单百分比。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 一天之前下达，但仍处于“未完成”状态（未取消或完成）的所有订单的列表。 |
| `Orders Per Hour (Past 7 Days)` | 按日按小时订购量。 |
| `Revenue Details (Past 30 Days)` | 将过去30天的每日收入细分为总收入值的所有组成部分。 |
| `Order Details by Coupon Code (Past 30 Days)` | 对于您的商店提供的每个优惠券代码，详细了解该优惠券代码的使用方式以及它在过去30天内引入的返回内容。 |
| `% Orders with Coupon (Past 30 Days)` | 过去30天内使用优惠券的订单与未使用优惠券的订单的百分比。 |

## 产品

“产品”仪表板显示从订购的产品、它们的商品总价值(GMV)以及购买和退款的热门产品等方面来说明的一般产品表现。 它可以帮助您平衡购买和回报，并确定产品成功和受欢迎程度。 您的商店必须[配置为跟踪退款](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html?lang=zh-Hans)，才能填充这些图表。

>[!NOTE]
>
>此仪表板上的报告可用于连接到具有任一配置类型（访客签出，无访客签出）的存储区的帐户。

### 报告

| 名称 | 描述 |
|---|---|
| `GMV (Past 30 Days)` | 过去30天销售的所有产品的商品总值。 GMV定义为每个产品的订购数量乘以基本价格。 |
| `% GMV (Past 30 Days) Refunded` | 过去30天内购买并导致退款的产品的GMV百分比。 |
| `Product Quantity Ordered (Past 30 Days)` | 过去30天内订购的物料总数。 |
| `% Purchased Products (Past 30 Days) Refunded` | 过去30天内购买并导致退款的项目百分比。 |
| `Gross Merchandise Value` | 按月份列出的所有已售产品的总商品价值。 GMV定义为每个产品的订购数量乘以基本价格。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 每项产品在过去30天内订购的总数与产品退款率的比较。 每个气泡的大小表示退款率。 |
| `Product Performance Details (Past 30 Days)` | 按产品SKU和产品名称列出过去30天内的销售及其后退款的详细信息。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 过去30天内销售的产品带来的收入最多（前10项）。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 在过去30天内购买的产品，因退款而损失的货物数量最多（前10个）。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 过去30天内销售的产品数量最多（前10个）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 在过去30天内购买导致最多退款的产品（前10项）。 |
