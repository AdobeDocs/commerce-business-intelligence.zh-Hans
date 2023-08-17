---
title: 克隆功能板
description: 了解如何克隆功能板。
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 克隆功能板

通过克隆功能板，您可以将功能板中的所有报表复制到新的功能板中。

如果要重新创建一组现有的图表，但更改视角（例如，不同的数据视图、不同的市场、不同的网站或商店），此方法非常有用。 复制仪表板后，可以编辑每个新图表以更改其量度、数据视图、过滤器或分组依据。

1. 要克隆功能板，请单击 **[!UICONTROL Options]** 在屏幕顶部。

1. 在下拉菜单中，单击 **[!UICONTROL Save As]**.

1. 出现提示时，输入 `New Dashboard Name`. Adobe会推荐一些名称，以便您一眼就知道仪表板中包含哪些信息。

   例如，您正在克隆名为的功能板 `Customer Activity`. 该仪表板包含有关您费城位置的客户活动信息，但现在您要为位于纽约市的位置创建一个仪表板。 此仪表板可以命名为 `New York City - Customer Activity`.

1. 使用 `Chart Title Find` 和 `Chart Title Replace` 用于查找所有图表的字段 `Philadelphia` 并将其替换为 `New York City`.

   如果您没有在这些字段中输入任何值， `(2)` 会在新仪表板中的所有图表标题末尾自动附加。

1. 单击 **[!UICONTROL Save]** 以克隆功能板。

示例：

![克隆功能板](../../assets/datgif.gif)
