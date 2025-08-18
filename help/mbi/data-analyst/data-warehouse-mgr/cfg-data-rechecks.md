---
title: 配置数据检查
description: 了解如何使用可变值配置数据列。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 配置数据检查

在数据库表中，可以存在具有可变值的数据列。 例如，在`orders`表中可能有一个名为`status`的列。 最初将订单写入数据库时，状态列可能包含值&#x200B;_pending_。 已在您的[Data Warehouse](../data-warehouse-mgr/tour-dwm.md)中使用此`pending`值复制该订单。

订单状态可以更改，但它们并不总是处于`pending`状态。 最终它可以变成`complete`或`cancelled`。 要确保Data Warehouse同步此更改，必须重新检查列以查找新值。

这如何与讨论的[复制方法](../data-warehouse-mgr/cfg-replication-methods.md)相适应？ 重新检查的处理方式因选择的复制方法而异。 `Modified\_At`复制方法是处理更改值的最佳选择，因为不必配置重新检查。 `Auto-Incrementing Primary Key`和`Primary Key Batch Monitoring`方法需要重新检查配置。

使用其中任一方法时，必须标记可更改列以重新检查。 可通过三种方法做到这一点：

1. 作为要重新检查的更新标志列的一部分运行的审核进程。

   >[!NOTE]
   >
   >审计人员依赖采样过程，并且可能不会立即捕获更改的列。

1. 您可以通过以下方式自行设置这些时间间隔：在Data Warehouse管理器中选中列旁边的复选框，单击&#x200B;**[!UICONTROL Set Recheck Frequency]**，然后为应检查更改的时间选择适当的时间间隔。

1. [!DNL Adobe Commerce Intelligence] Data Warehouse团队的成员可以在Data Warehouse中手动标记要重新检查的列。 如果您知道可更改列，请与团队联系以请求设置重新检查。 在您的请求中包含列列表以及频率。

## 重新检查频率 {#frequency}

**您知道吗？**
对`primary key`列设置重新检查不会检查该列是否有更改的值。 将检查表中是否包含已删除的行，并且所有已删除行都会从Data Warehouse中清除。

当列被标记为要重新检查时，您还可以设置重新检查的频率。 如果特定列不经常更改，则选择不太频繁的重新检查可以[优化更新周期](../../best-practices/reduce-update-cycle-time.md)。

频率选项包括：

* `always` — 在每次更新期间进行重新检查
* `daily` — 对您声明的时区在午夜后第一次更新进行重新检查
* `weekly` — 对于您声明的时区，在每周的9点后于星期五更新中进行重新检查
* `monthly` — 对于您声明的时区，每四周在星期五晚上9点后进行重新检查
* `once` — 仅在下次更新（一次性刷新）时发生

由于更新时间与需要同步的数据量相关，因此Adobe建议选择`daily`、`weekly`或`monthly`重新检查，而不是每次更新。

## 管理重新检查频率 {#manage}

通过单击表名称，然后检查各个列，可以在Data Warehouse中管理重新检查频率。 同步状态和重新检查频率(**是否更改？**&#x200B;列)。

要更改重新检查频率，请单击要更改的列旁边的复选框。 然后单击&#x200B;**[!UICONTROL Set Recheck Frequency]**&#x200B;下拉菜单并设置所需的频率。

![](../../assets/dwm-recheck.png)

您有时可能会在`Paused`列中看到`Changes?`。 当表的[复制方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)设置为`Paused`时，将显示此值。

[!DNL Adobe]建议查看这些列以优化更新并确保重新检查可更改的列。 如果根据数据更改的频率，列的重新检查频率很高，Adobe建议减少它以优化更新。

如有疑问，请联系我们，或者查询当前的复制方法或重新检查。

**相关：**

* [减少更新时间](../../best-practices/reduce-update-cycle-time.md)
* [优化数据库以进行分析](../../best-practices/opt-db-analysis.md)
