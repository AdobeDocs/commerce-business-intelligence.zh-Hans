---
title: 了解 [!DNL Commerce Intelligence] 环境
description: 了解如何使用和改进 [!DNL Commerce Intelligence] 环境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# 您的[!DNL Adobe Commerce Intelligence]环境

在分析商业数据时，请注意这些因素和常见的误解。 如果需要有关确保正确使用Commerce架构的帮助，请立即[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## [!DNL entity\_id]

许多表包含名为`entity\_id`的列。 在每个包含`entity\_id`的表中，该列用于标识唯一行。

例如，`sales\_order`表中的每一行都是唯一的顺序。 此表中的主键名为`entity\_id`。 可将此列视为`order\_id`。 在单独的表`customer\_entity`中，每一行表示一个唯一的客户。 此表中的主键也称为`entity\_id`，可以将其视为`customer\_id`。

在这些表中，`sales\_order.entity\_id`不等于`customer\_entity.entity\_id`。 这适用于包含`entity\_id`的所有表集： `table\_A.entity\_id`不等于`table\_B.entity\_id`。

## [!DNL Guest orders]

如果您允许客户在没有帐户的情况下从您的网站订购（访客订单），则这些客户不会在`customer\_entity`表中填充为行。 此外，来宾下出的每个订单在`customer\_id`表中都有一个null `sales\_order`值。

因此，如果您希望跟踪来宾在一段时间内的行为，则必须在`sales\_order`表中使用客户标识符（如`customer\_email`）计算所有客户级别的列。

如果您将`sales\_order`表用作customer表，则在创建客户级量度时必须小心。 例如，考虑平均生命周期收入量度。 此量度用于标识整个客户群的平均生命周期收入。 首先，需要新列，对于每个客户，此列将返回其生命周期收入。 然后，您必须对此列求平均值，以获取客户的平均生命周期收入。

如果您能够使用`customer\_entity`表，则每行是一个客户，并且该表中每个客户仅存在一次。 因此，当您具有存留期收入列时，您只需创建一个平均量度。 但是，如果您使用`sales\_order`表作为customer表，则客户可能会存在于许多行中。 设置存留期收入列后，给定客户下达的每张订单（行）将显示该客户的存留期收入；但您只想在总体平均量度中包含该客户一次。

这里的技巧是，您必须向量度添加一个过滤器，以确保只包含每个客户一次。 Adobe鼓励您创建并使用名为&#x200B;**我们计算的客户**&#x200B;的筛选器集，该筛选器集过滤了&#x200B;**客户的订单号= 1**（您可能需要排除不需要的客户的其他筛选器）。 添加此过滤器可确保每个客户在客户级别的量度中仅包含一次。

## 产品和类别

产品可以有多个类别，而类别可用于多个产品。 因此，在设置类别级别分析时，必须使用正确的定义。 是否要顶级类别？ 第二级类别？ 如果产品可能属于多个顶级类别，该怎么办？

试想一下，根据Commerce的实施，有一条牛仔裤属于三个不同的等级：“服装”（顶级）、“外套”（第二级）和“裤子”（第三级）。 您可能希望按售出件数分析类别性能。 此分析所需的量度是&#x200B;_销售的项目_，它基于`sales\_order\_item`表构建。 因此，您需要将类别级别的信息移动到项表中。 `sales\_order\_item`表上的每一行都有一个关联的`product\_id`，因此，如果您知道与产品关联的类别，则可以将该信息带到所需的表。

在移动任何数据之前，必须首先了解正确的连接和过滤器，以确保获取正确的类别。 对于某些分析，您可能需要知道“裤子”，但在其他分析中，“服装”可能更合适。 这些是单独标识的不同类别。 了解每个类别级别的定义方式可确保您将单位销售量归因到特定分析的相应类别。

现在，假设您的网站主页中还有`Our Favorites`顶级类别。 您可能已经实施了Commerce商店，以便将这些牛仔裤同时包含在`Clothing`类别和`Our Favorites`类别中。 如果是这样的话，这条牛仔裤不止一个顶级类别。 在这种情况下，将单个顶级类别移至`sales\_order\_item`表不太合理，因为有多个选项。 为此，Adobe建议创建可检查特定类别的“是”/“否”列。 例如，`Is product in Clothing category?`和`Is product in Our Favorites category?`列允许您检查产品是否属于这些特定类别。
