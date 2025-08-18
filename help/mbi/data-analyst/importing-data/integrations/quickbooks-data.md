---
title: 预期的QuickBooks数据
description: 了解如何轻松地跟踪相关数据字段以供分析。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 预期[!DNL QuickBooks]数据

在连接[您的 [!DNL QuickBooks] 帐户](../../../data-analyst/importing-data/integrations/quickbooks.md)后，您可以使用[Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)轻松跟踪相关数据字段以供分析。 将在Data Warehouse中创建以下表：

要查看所有可用于跟踪的字段，请单击表名列中的链接。

## 交易实体 {#transactionentities}

| **表名** | **描述** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | `bills`表包含有关AP交易的信息或来自第三方的付款请求。 属性包括货币类型、汇率、总额、到期日、余额等。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment`实体是从供应商收到的票据的最终付款交易记录。 此表包括供应商信息、付款类型、总额、交易记录日期等。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | `creditmemos`表记录全部和部分付款的退款或贷项交易记录。 某些属性包括客户名称、客户的帐单和送货信息、金额和日期。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits`包括直接存款和存放在`Undeposited Funds`帐户后移入资产帐户的客户付款。 属性包括金额、存款ID和日期。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates`是提供给客户的交易，包括商品或服务的建议定价。 此表记录金额、任何折扣信息、客户信息和日期。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices`是客户稍后支付的销售表单。 发票表记录所有存款信息、日期、行项目、税务信息和客户信息。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | `journalentries`表记录AR和AP帐户信息，包括日记帐条目ID、交易日期和行项目信息。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | `payment`记录包括付款ID、已核销和未核销金额、交易日期、交易类型和处理状态等属性。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | `purchases`表表示您的支出，包括购买ID、付款类型、金额和任何行项目信息。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | `purchaseorders`表保存发送给供应商的货物请求。 此表包括供应商信息、采购订单ID、交易记录日期、行项目信息、总金额和AP帐户信息。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | `refundreceipts`表记录给客户的退款。 属性包括退款收款ID、行项目信息、总金额、客户信息和余额。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | `salesreceipts`表记录提供给客户的销售收款中的信息，包括销售收款ID、行项目信息、总额、客户信息、交易日期和任何定金。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | `timeactivities`表保存供应商和/或员工的时间记录，包括时间活动ID、员工/供应商信息、记录的时间、活动描述和记录的日期。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | `transfers`表记录帐户之间移动的资金信息。 属性包括转帐ID、金额、帐户信息和日期。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 供应商贷项是退款或提供给供应商贷项的AP交易记录。 `vendorcredits`表包括供应商贷项ID、行项目信息、供应商信息、AP帐户、总金额和日期。 |

{style="table-layout:auto"}

## 命名列表实体 {#namelistentities}

| **表名** | **描述** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | 此表包括帐户ID、名称、状态、类型、余额、货币和创建时间。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | 此表记录与公司预算相关的所有信息，包括预算ID、名称、起始日期和终止日期、类型、状态和详细信息。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | 类应用于事务处理的明细行，使您能够跟踪未与客户或项目关联的区段。 此表记录类ID、名称、子类和状态。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | `customers`表包含与您的客户相关的所有信息，包括客户的ID、姓名、帐单和送货地址、电话号码和电子邮件地址。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | `departments`表包括部门ID、名称和类型（子部门与顶层部门）。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | `employees`表记录有关您公司员工的信息。 如果公司启用了工资单，则属性包括员工ID、姓名、地址、电话号码和可记帐信息。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | `items`表包含有关贵公司销售的产品或服务的详细信息。 此表包括物料标识、名称、说明、单价、类型、采购信息、现有量以及收入和资产帐户信息。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | `paymentmethods`表记录收到的商品和服务的付款方式。 它包含付款ID、类型和名称。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | 此表记录有关税务代理的信息（包括税务代理ID），以及有关采购和销售税的跟踪信息。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 税码用于跟踪产品、服务和客户的纳税状态（应纳税与不纳税）。 `taxcodes`表包括税码ID、名称、描述、状态、应纳税状态、税率和税组。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 税率用于计算税项负债。 此表包括税率ID、名称、说明、税率、税务代理等。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | 此实体指销售条款。 术语表包括术语ID、名称、类型、折扣百分比和截止日期。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 供应商表包含有关您从中购买的供应商的信息。 表属性包括供应商ID、公司名称、帐号、帐户余额、1099状态、帐单地址、电话号码、电子邮件地址和网址。 |

{style="table-layout:auto"}

## 相关：

* [正在连接 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
