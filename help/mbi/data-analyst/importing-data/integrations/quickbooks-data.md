---
title: 预期QuickBooks数据
description: 了解如何轻松跟踪相关数据字段以进行分析。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# 预期 [!DNL QuickBooks] 数据

![](../../../assets/Quickbooks.png)

之后 [您已连接 [!DNL QuickBooks] 帐户](../../../data-analyst/importing-data/integrations/quickbooks.md)，则可以使用 [data warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以轻松跟踪相关数据字段进行分析。 将在您的data warehouse中创建以下表：

要查看所有可用于跟踪的字段，请单击表名称列中的链接。

## 交易实体 {#transactionentities}

| **表名称** | **描述** |
|-----|-----|
| [`bill`](https://developer.intuit.com/docs/api/accounting/Bill) | 帐单表包含有关AP事务处理或第三方付款请求的信息。 属性包括币种类型、汇率、总金额、到期日、余额等。 |
| [`billpayments`](https://developer.intuit.com/docs/api/accounting/BillPayment) | 票据付款实体是从供应商处收到的票据付款的最终事务处理。 此表包括供应商信息、付款类型、总金额、交易日期等。 |
| [`creditmemos`](https://developer.intuit.com/docs/api/accounting/CreditMemo) | 贷项通知单表记录全部和部分付款的退款或贷项交易记录。 某些属性包括客户的名称、客户的账单和送货信息、金额和日期。 |
| [`deposits`](https://developer.intuit.com/docs/api/accounting/Deposit) | 存款包括直接存款及客户款项，该等款项于资产账户持有 `Undeposited Funds` 帐户。 属性包括金额、存款ID和日期。 |
| [`estimates`](https://developer.intuit.com/docs/api/accounting/Estimate) | 估算是指向客户提供的交易，包括建议的商品或服务的定价。 此表记录金额、任何折扣信息、客户信息和日期。 |
| [`invoices`](https://developer.intuit.com/docs/api/accounting/Invoice) | 发票是客户以后支付的销售表单。 发票表记录所有存款信息、日期、行项目、税务信息和客户信息。 |
| [`journalentries`](https://developer.intuit.com/docs/api/accounting/JournalEntry) | 日记帐分录表记录AR和AP帐户信息，包括日记帐分录ID、事务处理日期和行项目信息。 |
| [`payments`](https://developer.intuit.com/docs/api/accounting/Payment) | 付款记录包括诸如付款ID、已核销和未核销金额、交易日期、交易类型和处理状态等属性。 |
| [`purchases`](https://developer.intuit.com/docs/api/accounting/Purchase) | 购买表表示您的费用，包括购买ID、付款类型、金额和任何行项目信息。 |
| [`purchaseorders`](https://developer.intuit.com/docs/api/accounting/PurchaseOrder) | 采购订单是发送给供应商的货物的请求。 此表包括供应商信息、采购订单ID、交易日期、行项目信息、总金额和AP帐户信息。 |
| [`refundreceipts`](https://developer.intuit.com/docs/api/accounting/RefundReceipt) | 此表记录给客户的退款。 属性包括退款收款ID、行项目信息、总金额、客户信息和余额。 |
| [`salesreceipts`](https://developer.intuit.com/docs/api/accounting/SalesReceipt) | 销售收据表记录提供给客户的销售收据中的信息，包括销售收据ID、行项目信息、总金额、客户信息、交易日期和任何存款。 |
| [`timeactivities`](https://developer.intuit.com/docs/api/accounting/TimeActivity) | 时间活动是供应商和/或员工的时间记录。 时间活动表包括时间活动ID、员工/供应商信息、记录的时间、活动描述和记录的日期。 |
| [`transfers`](https://developer.intuit.com/docs/api/accounting/Transfer) | 转帐表记录有关在帐户之间转移的资金的信息。 属性包括转移ID、金额、帐户信息和日期。 |
| [`vendorcredits`](https://developer.intuit.com/docs/api/accounting/VendorCredit) | 供应商贷项是指向供应商退款或贷项的AP交易记录。 的 `vendorcredits` 表包括供应商信用ID、行项目信息、供应商信息、AP帐户、总金额和日期。 |

{style=&quot;table-layout:auto&quot;}

## 名称列表实体 {#namelistentities}

| **表名称** | **描述** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/docs/api/accounting/Account) | 此表包括帐户ID、名称、状态、类型、余额、币种和创建时间。 |
| [`budgets`](https://developer.intuit.com/docs/api/accounting/Budget) | 此表记录与公司预算有关的所有信息，包括预算ID、名称、开始和结束日期、类型、状态和详细信息。 |
| [`classes`](https://developer.intuit.com/docs/api/accounting/Class) | 类应用于事务处理明细行，允许您跟踪未与客户端或项目绑定的区段。 此表记录类ID、名称、子类和状态。 |
| [`customers`](https://developer.intuit.com/docs/api/accounting/Customer) | “客户”表包含与您的客户相关的所有信息，包括客户的ID、姓名、帐单和送货地址、电话号码和电子邮件地址。 |
| [`departments`](https://developer.intuit.com/docs/api/accounting/Department) | 部门表包括部门ID、名称和类型（子部门与顶级部门）。 |
| [`employees`](https://developer.intuit.com/docs/api/accounting/Employee) | 员工表记录有关为贵公司工作的人员的信息。 属性包括员工ID、姓名、地址、电话号码和可计费信息（如果公司启用了工资单）。 |
| [`items`](https://developer.intuit.com/docs/api/accounting/Item) | 项目表包含有关贵公司所销售产品或服务的详细信息。 此表包括物料ID、名称、说明、单价、类型、采购信息、现有量以及收入和资产帐户信息。 |
| [`paymentmethods`](https://developer.intuit.com/docs/api/accounting/PaymentMethod) | Paymentmethods表记录了为货物和服务收到的付款方式。 它包含付款ID、类型和名称。 |
| [`taxagencies`](https://developer.intuit.com/docs/api/accounting/TaxAgency) | 此表记录了有关税务机构的信息，包括税务机构ID，以及有关采购和销售税的跟踪信息。 |
| [`taxcodes`](https://developer.intuit.com/docs/api/accounting/TaxCode) | 税码用于跟踪产品、服务和客户的税状态（应税与非应税）。 税码表包括税码标识、名称、说明、状态、应纳税状态、税率和税组。 |
| [`taxrates`](https://developer.intuit.com/docs/api/accounting/TaxRate) | 税率乃用于计算税项负债。 此表包括税率标识、名称、说明、税率、税务代理等。 |
| [`terms`](https://developer.intuit.com/docs/api/accounting/Term) | 此实体指进行销售的条款。 术语表包括术语ID、名称、类型、折扣百分比和到期日。 |
| [`vendors`](https://developer.intuit.com/docs/api/accounting/Vendor) | 供应商表包含您从中购买的供应商的相关信息。 表属性包括供应商ID、公司名称、帐号、帐户余额、1099状态、帐单地址、电话号码、电子邮件地址和网址。 |

{style=&quot;table-layout:auto&quot;}

## 相关：

* [连接 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
