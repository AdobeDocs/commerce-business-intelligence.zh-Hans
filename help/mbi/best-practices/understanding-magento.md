---
title: 了解您的 [!DNL Commerce Intelligence] 环境
description: 了解如何使用和改进您的 [!DNL Commerce Intelligence] 环境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# 您的 [!DNL Adobe Commerce Intelligence] 环境

在分析商业数据时，请注意这些因素和常见的误解。 如果您在确保正确使用Commerce架构方面需要帮助，请立即 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

许多表都包含名为的列 `entity\_id`. 在每个包含 `entity\_id`，该列用于标识唯一行。

例如， `sales\_order` 表格是一个唯一顺序。 此表的主键名为 `entity\_id`. 本专栏可被认为是 `order\_id`. 在一个单独的表格中， `customer\_entity`，每一行表示一个唯一的客户。 此表中的主键也称为 `entity\_id`，可以将其视为 `customer\_id`.

在那些表格里， `sales\_order.entity\_id` 不等于 `customer\_entity.entity\_id`. 对于包含以下项的所有表集，此情况都为true `entity\_id`： `table\_A.entity\_id` 不等于 `table\_B.entity\_id`.

## [!DNL Guest orders]

如果您允许客户在没有帐户的情况下从您的网站订购（访客订单），则这些客户不会在 `customer\_entity` 表格。 此外，访客下单的每个订单都为空 `customer\_id` 值 `sales\_order` 表格。

因此，如果您希望跟踪来宾在一段时间内的行为，所有客户级别的列都必须根据 `sales\_order` 表，使用客户标识符，例如 `customer\_email`.

如果您使用 `sales\_order` 表，则在创建客户级别量度时必须小心。 例如，考虑平均生命周期收入量度。 此量度用于标识整个客户群的平均生命周期收入。 首先，需要新列，以便为每个客户返回其生命周期收入。 然后，您必须对此列求平均值，以获取客户的平均生命周期收入。

如果您能够使用 `customer\_entity` 表，每一行都是一个客户，并且每个客户仅在该表中存在一次。 因此，当您具有生命周期收入列时，您只需创建一个平均量度。 但是，如果您使用 `sales\_order` 表作为客户表，客户可能存在于许多行中。 设置生命周期收入列后，给定客户下达的每个订单（行）将显示该客户的生命周期收入；但您只想在总体平均量度中包含该客户一次。

这里的技巧是，您必须向量度添加一个过滤器，以确保只包含每个客户一次。 Adobe鼓励您创建并使用名为的过滤器集 **我们计算的客户** 筛选条件 **客户的订单编号= 1** （在排除不需要的客户时，您可能需要使用其他过滤器）。 添加此过滤器可确保每个客户在客户级别的量度中仅包含一次。

## 产品和类别

产品可以有多个类别，而类别可用于多个产品。 因此，在设置类别级别分析时，必须注意使用正确的定义。 是否要顶级类别？ 二级类别？ 如果产品可以归入多个顶级类别，该怎么办？

想象一下，根据Commerce实施中的定义，一条牛仔裤分为三个不同的类别级别：“服装”（顶级）、“外套”（第二级）和“裤子”（第三级）。 您可能希望按售出件数分析类别性能。 此分析所需的量度是 _已售出商品_，构建于 `sales\_order\_item` 表格。 因此，您需要将类别级别的信息移动到物料表中。 上的每一行 `sales\_order\_item` 表具有关联的 `product\_id`，因此，如果您知道与产品关联的类别，则可以将该信息转到所需的表中。

在移动任何数据之前，您必须首先知道正确的联接和过滤器，以确保获取正确的类别。 对于某些分析，您可能需要知道“裤子”，但在其他分析中，“服装”可能更合适。 这些是单独标识的不同类别。 了解每个类别级别的定义方式可确保您将单位销售量归因到特定分析的相应类别。

现在，想象一下 `Our Favorites` 网站主页上的顶级类别。 您可能已经实施了Commerce商店，以便在这两个商店中都包含这些牛仔裤 `Clothing` 类别和 `Our Favorites` 类别。 如果是这样的话，这双牛仔裤还有多个顶级类别。 在这种情况下，将单个顶级类别移至 `sales\_order\_item` 表格不太合理，因为有多种选择。 为此，Adobe建议创建可检查特定类别的“是”/“否”列。 例如， `Is product in Clothing category?` 和 `Is product in Our Favorites category?` 列允许您检查产品是否属于这些特定类别。
