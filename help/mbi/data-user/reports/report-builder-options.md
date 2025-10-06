---
title: 选择一个Report Builder
description: 了解如何选择Report Builder。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# 选择一个Report Builder

>[!NOTE]
>>需要[管理员权限](../../administrator/user-management/user-management.md)。

现在，您有了更多创建分析的选项，有时可能很难确切知道哪种Report Builder风格适合您的需求。 本主题将指导您选择构建分析的最佳方法。

## 何时应使用[!DNL SQL Report Builder]？ {#whensql}

查看一些在[!DNL SQL Report Builder]上使用[!DNL traditional Report Builder]的更常见原因。

### 如果要使用特定于[!DNL SQL]的函数……

[!DNL SQL Report Builder]的优点之一是，它使您能够使用Data Warehouse管理器中当前未提供的功能。 过去，分析师可能必须介入以帮助您充分实现您的愿景。

[!DNL SQL Report Builder]支持[`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html)和[`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)等以前无法使用的函数。 您可以访问[`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但某些其他特定于SQL的函数包括：

* [`Bitwise aggregate`个函数](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation`操作员](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果你想做些测试……

如果您想尝试不同的技术和策略来找出最适合您的分析的方法，您可能需要使用[!DNL SQL Report Builder]。 在Data Warehouse Manager中构建列需要时间和使用DWM创建的列，具体取决于更新周期。

您最多只能等待一个更新周期，然后才能使用列。 如果您意识到在构建列时出错，则必须等待&#x200B;*两个*&#x200B;周期：一个最初填充该列，另一个周期用于传播修订。

### 如果只使用新列一次……

如上一节中所述，在Data Warehouse Manager中创建列需要一些时间。 如果您只打算在一个报表中使用您创建的列，Adobe建议使用[!DNL SQL Report Builder]。 这无需等待更新周期完成，从而让您更快地恢复工作。

### 如果您使用的数据具有一对多关系……

有时，数据结构可能会使[!DNL SQL Report Builder]成为构建分析时更有效、更合理的选择。 在Data Warehouse Manager中为一对一关系创建列非常简单，但在处理一对多关系时，可能会遇到一些令人困惑的情况。

假设单个产品被视为属于多个产品类别，并且您希望查看与每个产品的每个类别关联的收入。 尝试使用DWM创建此关系可能既繁琐又困难，但编写[!DNL SQL]查询可能更简单一些：

![SQL查询显示具有一对多关系的产品类别收入](../../assets/When_should_I_use_the_RB_2.png)

## 何时应使用传统Report Builder？ {#whentraditionalrb}

虽然[!DNL SQL Report Builder]为您提供了对以前不可用功能的更多控制和访问权限，但它可能并不总是正确的选择。 Adobe建议，在确定要使用的Report Builder的风格时，也应考虑以下事项。

### 如果您正在构建一个简单的报表……

如果要创建的查询很简单，则使用传统Report Builder的速度可能比编写完整[!DNL SQL]查询快得多。 如果您需要创建分析的任何列已在Data Warehouse Manager中，则此功能会很有用。

### 如果您正在与其他用户共享您的工作……

贵组织中的用户是否使用/查看此分析？ 根据您正在与谁共享您的工作，有时候使用可视化Report Builder可能会更好。 与读取可能较长的[!DNL Visual Report Builder]查询相比，用户可以快速查看[!DNL SQL]中的定义。

如果有人需要报告但不熟悉[!DNL SQL]，Adobe建议使用Report Builder的原始风格。 这样他们就可以轻松办事。

## 正在结束 {#wrapup}

[!DNL SQL Report Builder]和[!DNL Visual Report Builder]都适用于各种用例。 这通常取决于您的分析需求以及谁在使用分析。
