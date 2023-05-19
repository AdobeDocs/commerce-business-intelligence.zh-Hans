---
title: 從SQL查詢建立視覺效果
description: 瞭解如何熟悉SQLReport Builder中使用的術語，並為您建立SQL視覺效果奠定堅實的基礎。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 從SQL查詢建立視覺效果

本教學課程的目標是讓您熟悉 [!DNL SQL Report Builder] 並為您建立虛擬報表奠定堅實的基礎 `SQL visualizations`.

此 [[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) 是具有選項的report builder：您可以僅為了擷取資料表目的而執行查詢，也可以將這些結果轉換為報表。 本教學課程說明如何從SQL查詢建立視覺效果。

## 術語

在開始本教學課程之前，請參閱以下在 `SQL Report Builder`.

- `Series`：您要測量的資料行在SQLReport Builder中稱為Series。 常見範例為 `revenue`， `items sold`、和 `marketing spend`. 至少必須有一個欄設定為 `Series` 以建立視覺效果。

- `Category`：您要用來劃分資料區段的欄稱為 `Category` 這就像是 `Group By` 中的功能 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). 例如，如果您想要依客戶贏取來源來劃分客戶的期限收入，則包含贏取來源的欄將會指定為 `Category`. 可將多個欄設為 `Category`.

>[!NOTE]
>
>日期和時間戳記也可作為 `Categories`. 它們只是查詢中的另一欄資料，且必須依查詢本身的需要加以格式化和排序。

- `Labels`：這些標籤會套用為x軸標籤。 分析一段時間的資料趨勢時，會將年和月欄指定為標籤。 可以將多個欄設定為Label。

## 步驟1：撰寫查詢

請牢記以下事項：

- 此 [!DNL SQL Report Builder] 使用 [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- 如果您要建立含有時間序列的報告，請務必 `ORDER BY` 時間戳記欄。 這可確保時間戳記在報表上的繪製順序正確。

- 此 `EXTRACT` 函式非常適合用於剖析時間戳記的日、周、月或年。 這在下列情況下相當實用： `time interval` 您要在報告上使用的是 `daily`， `weekly`， `monthly`，或 `yearly`.

若要開始使用，請開啟 [!DNL SQL Report Builder] 按一下 **[!UICONTROL Report Builder** > **SQL Report Builder]**.

例如，假設此查詢傳回每個產品每月的銷售專案總數：

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

此查詢會傳回此結果表格：

![](../assets/SQL_results_table.png)

## 步驟2：建立視覺效果

有了這些結果， *如何建立視覺效果？* 若要開始使用，請按一下 **[!UICONTROL Chart]** 索引標籤中的 `Results` 窗格。 這會顯示 `Chart settings` 標籤。

第一次執行查詢時，報表可能看起來不可預測，因為查詢中的所有欄都繪製為序列：

![](../assets/SQL_initial_report_results.png)

在此範例中，您希望這會是隨時間呈現趨勢的折線圖。 若要建立，請使用下列設定：

- `Series`：選取 `Items sold` 欄作為 `Series` 因為您想要測量它。 定義 `Series` 欄中，您會看到報表中繪製了一行。

- `Category`：在此範例中，您想要以報表中不同的行檢視每個產品。 若要這麼做，請設定 `Product name` 作為 `Category`.

- `Labels`：使用欄 `year` 和 `month` 作為x軸上的標籤以便檢視 `Items Sold` 隨著時間推移成為趨勢。

>[!NOTE]
>
>查詢必須包含 `ORDER BY` 標籤上的子句(如果它們是 `date`/`time` 欄。

以下快速瞭解您如何建立此視覺效果，從執行查詢到設定報表：

![](../assets/SQL_report_settings.gif)

## 步驟3：選取 `Chart Type`

此範例使用 `Line` 圖表型別。 使用不同的 `chart type`，按一下圖表選項區段上方的圖示進行變更：

![](../assets/Chart_types.png)

## 步驟4：儲存視覺效果

如果您想要再次使用此報表，請為報表命名，然後按一下 **[!UICONTROL Save]** 右上角。

在下拉式清單中，選取 `Chart` 作為 `Type` 然後是要儲存報表的控制面板。

## 正在結束

想要更進一步嗎？ 檢視 [查詢最佳化最佳實務](../best-practices/optimizing-your-sql-queries.md).
