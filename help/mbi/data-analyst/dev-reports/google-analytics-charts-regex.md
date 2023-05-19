---
title: 建立Google Analytics圖表
description: 瞭解如何從Google Analytics資料建立圖表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 建立 [!DNL Google Analytics] 圖表

（含規則運算式語法說明）

在您連線至 [[!DNL Google Analytics] 帳戶](../../data-analyst/importing-data/integrations/google-analytics.md)，您可以透過以下專案建立圖表： [!DNL Google Analytics] 資料。

## 建立 [!DNL Google Analytics] 圖表

1. 按一下 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 在中選取量度時 `Chart Builder`，捲動至清單底部以尋找包含下列專案的區段： [!DNL Google Analytics] 設定檔。 第二個量度下拉式清單隨即顯示。 您可以在此處選擇要分析的量度。

1. 選擇量度後，您可以選取「 」，將此圖表當成任何其他圖表來處理 `time period`， `interval`、和資料 `perspectives` 您希望看到的專案。

1. 這裡有一個主要差異 `√` 篩選器使用規則運算式。 規則運算式（簡稱regex）是用於描述搜尋模式的特殊文字字串。 請參閱規則運算式語法範例： [[!DNL Google] Analytics規則運算式指南](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>唯一需要使用\字元逸出的特殊字元為下列中繼字元：

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
