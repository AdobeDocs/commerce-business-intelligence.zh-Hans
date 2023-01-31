---
title: 创建Google Analytics图
description: 了解如何根据Google Analytics数据创建图表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 创建 [!DNL Google Analytics] 图表

（包含正则表达式语法帮助）

在您连接了 [[!DNL Google Analytics] 帐户](../../data-analyst/importing-data/integrations/google-analytics.md)，则可以从 [!DNL Google Analytics] 数据。

## 创建 [!DNL Google Analytics] 图表

1. 单击 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 在 `Chart Builder`，滚动到列表底部以查找包含 [!DNL Google Analytics] 用户档案。 将显示第二个量度下拉列表。 在此，您可以选择要分析的量度。

1. 选择量度后，您可以继续处理此图表，就像它是任何其他图表一样，方法是选择 `time period`, `interval`和数据 `perspectives` 你想看的。

1. 这里的一个主要区别是 `√` 对过滤器使用正则表达式。 正则表达式（简称为正则表达式）是用于描述搜索模式的特殊文本字符串。 请参阅 [[!DNL Google] Analytics正则表达式指南](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>需要使用\字符进行转义的唯一特殊字符是以下元字符：

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
