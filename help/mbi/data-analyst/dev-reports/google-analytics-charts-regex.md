---
title: 创建Google Analytics图表
description: 了解如何根据Google Analytics数据创建图表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 创建 [!DNL Google Analytics] 图表

（使用正则表达式语法帮助）

在您连接 [[!DNL Google Analytics] 帐户](../../data-analyst/importing-data/integrations/google-analytics.md)之后，您便能够从 [!DNL Google Analytics] 数据。

## 创建 [!DNL Google Analytics] 图表

1. 单击 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 在中选择指标时 `Chart Builder`，滚动到列表底部以查找包含 [!DNL Google Analytics] 配置文件。 第二个量度下拉列表随即出现。 您可以在此处选择要分析的量度。

1. 选择量度后，您可以通过选择 `time period`， `interval`和数据 `perspectives` 您希望看到的内容。

1. 这里的一个主要区别是 `√` 使用正则表达式进行筛选。 正则表达式（简称regex）是用于描述搜索模式的特殊文本字符串。 请参阅中的正则表达式语法示例 [[!DNL Google] Analytics正则表达式指南](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>唯一需要使用\字符转义的特殊字符是下面的元字符：

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
