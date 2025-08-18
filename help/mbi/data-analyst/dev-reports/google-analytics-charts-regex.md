---
title: 创建Google Analytics charts
description: 了解如何根据Google Analytics数据创建图表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 创建[!DNL Google Analytics]个图表

（使用正则表达式语法帮助）

连接[[!DNL Google Analytics] 帐户](../../data-analyst/importing-data/integrations/google-analytics.md)后，即可使用[!DNL Google Analytics]数据创建图表。

## 创建[!DNL Google Analytics]个图表

1. 单击&#x200B;**[!UICONTROL Add Chart** > **Create New Chart]**。

1. 在`Chart Builder`中选择量度时，滚动到列表底部以查找包含[!DNL Google Analytics]配置文件的部分。 此时将显示第二个量度下拉列表。 您可以在此处选择要分析的量度。

1. 选择量度后，您可以通过选择想要查看的`time period`、`interval`和数据`perspectives`，像处理任何其他图表一样处理此图表。

1. 此处的主要区别是`√`使用正则表达式进行筛选。 正则表达式（简称regex）是用于描述搜索模式的特殊文本字符串。 请参阅[[!DNL Google] Analytics正则表达式指南](https://support.google.com/analytics/answer/1034324?hl=en)中的正则表达式语法示例。

>[!NOTE]
>
>唯一需要使用\字符转义的特殊字符是下面的元字符：

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
