---
title: 管理Adobe Commerce使用者和許可權
description: 瞭解如何管理您的Commerce Intelligence使用者。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 管理使用者許可權

[!DNL Adobe Commerce Intelligence] 旨在作為整個組織的單一信任來源。 每個使用者都有自己的儀表板集，他們可以 [與其他使用者共用](../../data-user/dashboards/share-dashboard-with-users.md).

## 使用者許可權層級

在 [!DNL Commerce Intelligence]，有三個一般許可權層級適用於使用者，這些層級會在建立帳戶時選取：

* `Admin`
* `Standard`
* `Read-Only`

這些許可權可讓使用者執行特定動作或存取特定部分 [!DNL Commerce Intelligence]. 下表列出每個許可權層級可執行的動作 [!DNL Commerce Intelligence]：

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **建立/管理使用者** | ✔ |  |  |
| **建立電子郵件摘要** | ✔ | ✔ |  |
| **建立/編輯/共用儀表板** | ✔ | ✔ |  |
| **檢視儀表板** | ✔ | ✔ | ✔ |
| **建立/編輯/刪除視覺化報表** | ✔ | ✔* |  |
| **建立/編輯/刪除SQL報告** | ✔ |  |  |
| **複製儀表板** | ✔ |  |  |
| **新增/管理整合** | ✔ |  |  |
| **存取Data Warehouse管理員** | ✔ |  |  |
| **同步/取消同步資料表和資料行** | ✔ |  |  |
| **建立/編輯量度** | ✔ |  |  |
| **建立/編輯篩選器集** | ✔ |  |  |
| **建立/編輯計算欄** | ✔ |  |  |
| **建立相依報表的清單** | ✔ |  |  |
| **存取系統摘要** | ✔ |  |  |
| **存取時區設定** | ✔ |  |  |
| **存取帳單** | ✔ | ✔** |  |
| **聯絡支援人員** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_您可以限制&#x200B;**[!UICONTROL Standard]**使用者的 [存取特定量度](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _使用者可以使用額外的許可權設定來存取帳單。_
>
>**[!UICONTROL Read-Only]** 使用者只能 _檢視_ 已與他們共用的儀表板；他們無法在中建立或編輯任何內容。 [!DNL Commerce Intelligence]，也無法搜尋控制面板並將其新增至帳戶。 Adobe建議您與共用一組特定的控制面板 **[!UICONTROL Read-Only]** 您或團隊其他成員維護的使用者。 請勿為其複製一組儀表板。

## 其他許可權：帳單與技術 {#billingtech}

除了一般許可權層級之外，還有另外兩個使用者指定存在 —  `Billing` 和 `Technical`. 這些指定應搭配一般許可權層級使用。

### 帳單

`Billing` 使用者有權存取帳單頁面，並可以變更付款資訊。 此外，Adobe也可能聯絡他們以詢問帳單問題。

`Admin` 使用者可以存取 `Billing` 定位字元，但 `Standard` 如果使用者擁有 `Billing` 核取方塊在其設定檔中選取。

![帳單](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` 使用者沒有任何針對他們的許可權 — 此設定只會標籤您組織內的技術連絡人。 Adobe可能會就技術問題聯絡這些使用者。

`Admin` 使用者可以按一下「 」，將新使用者新增至其帳戶 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 並依照提示進行。 在中建立使用者後 [!DNL Commerce Intelligence]，您邀請的幸運兒將會收到有關如何完成帳戶設定流程的電子郵件指示。

任何時候， `Admins` 按一下「 」，即可檢視其帳戶中的所有使用者 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. 此頁面顯示使用者的許可權以及他們可以存取的量度和儀表板。
