---
title: 选择报表生成器
description: 了解如何选择报表生成器。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# 选择报表生成器

>[!NOTE]
>>需要 [管理员权限](../../administrator/user-management/user-management.md).


我们都喜欢有选择。 但是，当面临选择时，我们中的一些人可能会对不得不做出决定的想法犹豫不决。 选择非常好，但也可能让人感到难以接受和困惑。

由于您有更多用于创建分析的选项，因此有时可能很难确切知道报表生成器的哪种口味适合您的需求。 如果您需要在选择构建分析的最佳方式方面提供一些指导，本文将为您提供相关帮助。

## 我应何时使用 `SQL Report Builder`? {#whensql}

请查看您使用SQLReport Builder而不是传统Report Builder的一些更常见原因。

### 如果要使用特定于SQL的函数……

的美 `SQL Report Builder` 是让您能够使用“Data warehouse管理器”中当前不可用的函数。 过去，分析师可能不得不介入，以帮助你充分实现自己的愿景。

SQLReport Builder支持诸如 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 和 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)，以前无法使用。 您可以访问 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但其他一些特定于SQL的函数包括：

* [`Bitwise aggregate` 函数](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 运算符](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果想要进行一些测试……

如果您想尝试使用不同的技术和策略来找出最适合分析的内容，则可能需要使用 `SQL Report Builder`. 在Data warehouse管理器中构建列需要时间，而使用DWM创建的列取决于更新周期。

至多，您必须等待一个更新周期，然后才能使用列。 如果你意识到自己在建柱子时犯了错误，你就得等一等 *二* 周期：一个用于最初填充列，另一个用于传播修订的周期。

### 如果只使用新列一次……

如上节中所述，在Data warehouse管理器中创建新列需要时间。 如果您只计划使用在一个报表中创建的列，我们建议您使用 `SQL Report Builder`. 这将无需等待更新周期完成，从而使您能够更快地返回工作。

### 如果您使用的数据具有一对多关系……

在某些情况下，数据的结构可能会使 `SQL Report Builder` 更高效、更符合逻辑的选择来构建分析。 在Data warehouse管理器中，为一对一关系创建列非常简单，但是在您处理一对多关系时，事情可能会有些混乱。

假设单个产品被视为多个产品类别的一部分，并且您希望查看与每个产品的每个类别关联的收入。 尝试使用DWM创建此关系可能既繁琐又困难，但编写SQL查询可能会比较简单：

![](../../assets/When_should_I_use_the_RB_2.png)

## 我何时应使用传统Report Builder? {#whentraditionalrb}

而 `SQL Report Builder` 让您能够更好地控制和访问以前不可用的功能，它可能并非总是正确的选择。 我们建议您在决定要使用报表生成器的哪种口味时，还应考虑以下事项。

### 如果您要构建简单的报表……

如果要创建的内容简单明了，则使用传统Report Builder比编写完整SQL查询要快得多。 如果需要创建分析的任何列已在Data warehouse管理器中，则此方法也将会有所帮助。

### 如果您要与其他用户共享您的工作……

贵组织中的用户是否会使用/查看此分析？ 根据您与谁共享您的工作，在某些情况下，继续使用可视化Report Builder可能会更好。 与读取可能较长的SQL查询相比，用户可以快速查看可视Report Builder中的定义。

如果有些人需要此报表，但不熟悉SQL，我们建议使用Report Builder的原始风格。 这会让他们更轻松。

## 包装 {#wrapup}

和 `SQL Report Builder` 和 `Visual Report Builder` 适合各种用例。 这通常取决于您的分析需求以及使用分析的人员。
