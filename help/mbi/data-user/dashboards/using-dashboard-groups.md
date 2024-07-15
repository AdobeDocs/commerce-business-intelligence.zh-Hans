---
title: 使用功能板组
description: 了解如何更好地组织功能板。
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 使用功能板组

仪表板组允许更好地组织仪表板。 最常见的用例是将类似的功能板分组到同一“组”下。 例如，所有与营销相关的功能板均可分组到功能板组“营销”下。

在仪表板选择下拉列表中，仪表板组按字母顺序显示，而“无组”下的所有仪表板最后显示。 同一组下的仪表板一起显示，并在每个组内按字母顺序显示。

## 仪表板组共享

无法在用户之间直接共享功能板组。 与用户共享功能板时，如果功能板不存在，则会自动为这些用户创建该功能板所属的功能板组。 如果仪表板组存在，则仪表板会附加到列表中。

当仪表板组的所有者更改该仪表板组时，更改将自动反映给与该仪表板共享的所有用户。 用户无法更改他们不拥有的仪表板的仪表板组。

## 创建功能板组

可以通过以下两种方式之一创建功能板组：

1. 创建功能板时：

   ![创建仪表板组](../../assets/create-dashboard-groups-new-dashboard.png)

1. 更改现有仪表板的组时，从`Manage Data > Dashboards`页面：

   1. 单击要创建组的仪表板。

   1. 在`Dashboard Group (optional)`下，将显示当前仪表板组。

   1. 要创建组，请键入新组的名称，然后单击框外部。

      ![创建仪表板组](../../assets/create-dashboard-groups-existing-dashboard.png)

## 将现有功能板添加到现有组

1. 在`Manage Data > Dashboards`页面上，选择要更改其组的仪表板。

1. `Dashboard Group (optional)`下的文本显示仪表板的当前仪表板组。

1. 要更改仪表板的组，请从列表中选择另一个组 — 在本例中为`PS`，`Campaigns`。

   ![更改组仪表板](../../assets/add-existing-dashboard-existing-group.png)

## 删除功能板组

当某个功能板组下方没有功能板时，该功能板组会被自动删除。
