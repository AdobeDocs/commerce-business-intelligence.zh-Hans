---
title: 回访间隔、频度、货币(RFM)分析
description: 了解如何设置功能板，以便您能够按客户最近、频度和货币排名对客户进行细分。
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# RFM分析

在本文中，我们将演示如何设置功能板，以便您根据客户的回访间隔、频度和货币排名对客户进行细分。 RFM分析是一种营销技术，它考虑客户行为，帮助您确定外联的区段。 它考虑了三个方面：最近客户从您的商店购买的次数、频度、从您那里购买的频率以及客户花费的货币。

![](../../assets/blobid0.png)

只有在具有 [!DNL MBI] Pro计划新架构(例如，如果“管理Data warehouse”菜单下有“视图”选项)。 这些列可以从“管理数据>Data warehouse”页面创建。 详细说明如下。

## 快速入门

您首先需要上载一个仅包含值为1的主键的文件。 这将允许为分析创建一些必要的计算列。

您可以利用此 [帮助中心文章](../importing-data/connecting-data/using-file-uploader.md) 以及下图来设置文件格式。

## 计算列

如果您的企业允许客人订购，则会有进一步的区别。 如果存在，则可以忽略 `customer_entity` 表。 如果不允许来宾订单，请忽略 `sales_flat_order` 表。

要创建的列

* **`Sales_flat_order/customer_entity`** 表
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* 已选择 [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       自客户上次订购日期后经过的秒数
   * [!UICONTROL Column type]: — “同一表>年龄
* 已选择 [!UICONTROL column]: `Customer's last order date`

* （输入）计数引用
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL输入]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL数据类型]: `Integer`

* **计数引用** 表（这是您刚才上传的文件，其编号为“1”）
* 客户数量
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` 或 `customer_entity.(input)reference > Count Reference`. `Primary Key`
* 已选择 [!UICONTROL column]: `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* **Customer_entity** 表
* 客户数量
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.（输入）参考>客户集中度。 `Primary Key`
* 已选择 [!UICONTROL column]: `Number of customers`

* （输入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* 按客户生命周期收入排名
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL数据类型]: `Integer`

* 客户的货币得分（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL数据类型]: `Integer`

* （输入）按客户生命周期订单数排名
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* 按客户生命周期订购数排名
* 
   [!UICONTROL列类型]: – "相同表>计算"
* [!UICONTROL Inputs]:- **（输入）按客户生命周期订单数排名**, **客户数量**
* [!UICONTROL Calculation]:- **当A为null时，则结束为null(B-(A-1))**
* [!UICONTROL Datatype]: — 整数

* 客户的频度分数（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL数据类型]: `Integer`

* 自客户上次订购日期后按秒数排名
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* 客户的回访间隔分数（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL数据类型]: `Integer`

* 客户的回访间隔分数（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL数据类型]: String

* **计数引用** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 已选择 [!UICONTROL column]: `sales_flat_order.customer_email` 或 `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 不等于000

* **Customer_entity** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 已选择 [!UICONTROL column]:- `Number of customers`

* 客户的回访间隔分数 `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL数据类型]: `Integer`

* （输入）按客户总体RFM得分排名
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 不等于000

* 按客户整体RFM得分排名
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL数据类型]: `Integer`

* 客户的RFM组
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL数据类型]: `Integer`

>[!NOTE]
>
>使用的百分比是客户的分割（例如，返回1-5的20%分段）。 如果您有自定义方式希望对这些值进行加权，请在提交票证时告知分析师。

## 量度

没有新量度！

**注意**:确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **按RFM分组的客户**
* 量度 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隐藏图表
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [!UICONTROL组依据]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最近5分的客户**
* 量度 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 隐藏图表
* 
   [!UICONTROL组依据]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **新近度得分为1的客户**
* 量度 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 隐藏图表
* 
   [!UICONTROL组依据]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与上面的示例功能板类似，但生成的三个表格只是您可以执行的客户分段类型的示例。
