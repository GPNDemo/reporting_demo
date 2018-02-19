---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - PHP
  - Java
  - javascript: Node.js
  - Ruby
  - REST
  - shell: cURL
  - SOAP

toc_footers:
  - Global Payments Powering Payments
  - <a href='https://www.globalpaymentsinc.com'>www.globalpaymentsinc.com</a>

includes:
  - errors

search: true
---

# Resourcessss
Resources ensure there is a common understanding of our product throughout our organisation and a common terminology when we communicate internally and to the market.  Resources inform the features we need to build to solve our customers’ problems.

Resources can have a **Status**, a **Type**, **Data** and **Relationships** to other resources. 

**Requests** are actions that are taken to affect Resources.

Each instance of a Resource has a unique **Global Payments ID**. This is a Global Payments reference that uniquely identifies the resource on the Global Payments system.



## Organisation

Organisations are typically businesses that have a contracted with Global Payments. Global Payments provides payment processing solutions to Organisations. Organisations can be Merchants, ISO, ISVs, VARs or Marketplaces. Organisations can be owned by Global Payments.

**Organisation Types**

***Type*** | ***Description***
-------------- | -------------- 
MERCHANT | An Organisation which has a contractual relationship with Global Payments for the provision of financial payment services, and/or technical payment services. 
MARKETPLACE | An Organisation which has a contractual relationship with Global Payments to resell or refer Global Payments' services. Merchants contract with Marketplaces.
ISO | Organisation which has a contractual relationship with Global Payments to resell or refer Global Payments' services. Merchants contract with ISOs.
 
**Organisation Statuses**

***Status*** | ***Description***
-------------- | -------------- 
CREATED | This indicates that an Organisation has been created. The Organisation cannot be used to process real payments until it is updated to a status of ACTIVE-LIVE. 
ACTIVE LIVE | This indicates that an Organisation  is in live mode can can be used to process real transactions.
ACTIVE TEST | This indicates that an Organisation is it test mode and that any activity against the Organisation  will be considered testing and real funds will never be processed.
DISABLED | This indicates that the Organisation  can no longer be used for payment processing. These resources are never deleted to maintain integrity and a record of historical activity. 
ERROR | Indicating that an Organisation  was not successfully created or updated. An example would be a required information missing resulting in an error when trying to create an Organisation.

**Organisation Requests** 
These are the actions that can be taken to a Global Payments Organisation.

### *create*
Used to create a new Organisation on Global Payments' system.

### *read*
Used to retrieve information about an existing Organisation.

### *update*
Used to update information about an existing Organisation.



## Account

A representation of a data needed to configure an Organisation to process payments. Typically this would information such as Organisation Deposit Bank Accounts, Allowed Functionality for that Account, Payment Method Specific details e.g. For Cards it would be the MID and TID.

**Account Types**

**Account Statuses**

***Status*** | ***Description***
-------------- | -------------- 
CREATED | This indicates that an Account has been created. It cannot be used to process real payments until it is updated to a status of ACTIVE-LIVE. 
ACTIVE LIVE | This indicates that an Account is in live mode can can be used to process real transactions.
ACTIVE TEST | This indicates that an Account is it test mode and that any activity against the Account will be considered testing and real funds will never be processed.
DISABLED | This indicates that the Account can no longer be used for payment processing. These resources are never deleted to maintain integrity and a record of historical activity. 
ERROR | Indicating that an Account was not successfully created or updated. An example would be a required information missing resulting in an error when trying to create an account for an Organisation.

**Account Requests**
These are the actions that can be taken to Global Payments Organisations' Accounts.

### *create*
Used to create a new Account on Global Payments' system

### *read*
Used to retrieve information about an existing Account.

### *update*
Used to update information about an existing Account.



## Transaction
An act to attempt the transfer of funds between the Customer and the Merchant. 

**Transaction Types**

***Type*** | ***Description***
-------------- | -------------- 
 PAYMENT | Payment is a transaction between a Customer and a Merchant in which the transfer of funds goes from the Customer to the Merchant
 REFUND | A Refund is a transaction between a Customer and a Merchant in which the transfer of funds goes from the Merchant to the Customer. There can be different types of Refund Transactions; for example ones that are linked to a previous Payment transaction and ones that are standalone. 
 

**Transaction Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 PREAUTHORISED | This indicates that the transaction was authorised successfully but has yet to be captured. Once Captured it will have a status of OPEN BATCH
 OPEN_BATCH | This indicates that the transaction was authorised successfully and automatically captured and is in an Open Batch ready to start the funding process once the Batch is closed.
 VOIDED | This indicates that the transaction was voided before it was Batched. Once Batched it cannot be cancelled
 BATCHED | This Status means that the transaction is now part of a closed Batch and it can no longer be Cancelled. If it has a Status of Batched it has started the process of being part of a Deposit in a  Merchants Bank account.
 DEPOSITED | This Status means that the transaction is now part of a Deposit that was sent to the Organisations bank account. The merchant now know they got money for this transaction.
 DISPUTED | This Status means that the transaction is being disputed by the Customer and the merchant may lose funds relating to this transaction if the Customer successfully contests the transaction.
 DECLINED | This indicates that the transaction did not processed successfully. The transaction was declined by the bank. 
 ERROR | Error represents a mistake in the request to execute a Transaction e.g. missing a mandatory field. 

**Transaction Requests**

### *authorise*
Organisation initiated request to Authorise a transaction. If authorised successfully and flagged for auto-capture then the transaction would be have an OPEN-BATCH Status.  If successfully authorised and not flagged for auto-capture then the transaction would be have a PREAUTHORISED Status. A separate capture request is needed to move the transactions from a PREAUTHORISED status to an OPEN-BATCH status.

### *cancel*
Organisation initiated request to void a transaction. This can be applied to successful authorised/preauthorised transactions and stops the transaction from going further in its' lifecycle.
This request must be executed before the Transaction has a status of BATCHED

### *refund*
Organisation initiated request to Refund a Customer money. This can be linked to an previous Payment transaction or a standalone where it does not link to a previous Payment Transaction.

### *adjust*
Organisation initiated request to change the amount of a transaction that has a status of PREAUTHORISED or OPEN-BATCH. e.g. to add a tip.
This request must be executed before the Transaction has a status of BATCHED

### *capture*
Organisation initiated request to start the process of moving funds between the Customer and the Organisation. It changes a transaction with a status of PREAUTHORISED to have a status of OPEN-BATCH. 

### *hold*
This is an organisation initiated request which If a transaction has an Open Batch status then putting it on hold removes it from the Open Batch but does not void the transaction. This could be used to pause a transaction for being processed in a Batch to check inventory or do fraud analysis

### *release*
If a Transaction has a current status of HELD then a release request will re-assign it a status of Open-Batch

### *force*
This is a request initiated by an Organisation that puts a transaction directly into an Open-Batch status and does not request an Authorisation/PreAuthorisation via the processor as the authcode has been attained elsewhere.

### *close-batch*
Where does this sit? Do we need a Batch Resource

### *read*
Used to retrieve information about an existing Transaction or group of Transactions.

### *update*
Used to update information about an existing Transaction. *Can this incorporate adjust, cancel, hold, release?*




## Deposit

The initiation of a Debit or a Credit to a Merchant's Bank Account that relates to Transactions and Disputes processed via Global Payments or fees charged by Global Payments to the Organisation. 

**Deposit Types**

***Type*** | ***Description***
-------------- | -------------- 
 SPLIT | The Deposit was paid partly to the Organisation and partly to a third party, based on a pre-agreed arrangement between the Organisation and the third party.
  
**Deposit Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 DELAYED | The Deposit is been held in a Global Payments account for a period of time before being transferred to an Organisation's account.
 RESERVED | The Deposit is been held in a Global Payments account where it will be reviewed before it is released to an Organisation's account.
 DEPOSITED | The Deposit has been initiated to an Organisation's bank account.
 
### *read*
Used to retrieve information about an existing Deposit or group of Deposits.
 
 
## Dispute

An act, initiated by the Customer or their bank, to get more information about that transaction or to challenge a transaction with a view to reverse the transfer of funds between that Customer and the Merchant.

**Dispute Types**

***Type*** | ***Description***
-------------- | -------------- 
 INQUIRY | An inquiry is a request for additional information on a transaction to validate the sale prior to the transaction being disputed. Normally the signed sales draft of the transaction is sufficient to resolve an inquiry request with the issuer. Not all disputes go through the inquiry phase first, majority of cardholder disputes are chargebacks and not retrievals. 
 CHARGEBACK | A dispute is created when a cardholder has a disagreement on a merchant processed transaction or the issuing bank has identified a transaction that was processed out of compliance. This results in a return of funds from the merchant to the cardholder. There can be many cycles of a dispute if the issuer and acquirer can't easily resolve the dispute case.  
 REPRESENTMENT |  A reversal of a previous chargeback where the merchant has provided sufficient evidence to challenge the chargeback that results in the funds being returned to the merchant.

**Dispute Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 OPEN | When a Dispute has been raised and merchant action is required.
 PENDING | When a Dispute is awaiting an update from the processor.
 CLOSED | The dispute has been finalised with a result indicating whether the merchant has been successful in challenging the 


**Dispute  Requests**

### *notify*
Global Payments will notify you of new disputes or changes to existing disputes with a status of PENDING.

### *challenge*
Organisation initiated request to provide evidence of a transaction related to a dispute.

### *read*
Organisation initiated request to return information related to a Dispute.

### *accept*
Organisation initiated request to accept a chargeback. An organisation understands that money has left their account related to the associated transaction and that the dispute cannot be challenged further by the organisation.




## Customer

A consumer or business, who does not typically have a contractual relationship with Global Payments, who wishes to engage in transactions with a Merchant. Customers buy products or services from a Merchant.


**Customer Types**

***Type*** | ***Description***
-------------- | -------------- 
 BUSINESS | The customer in this case is a business and is involved in a B2B relationship with a Global Payments' Organisation. 
 CONSUMER | The customer in this case is a consumer and is involved in a B2C relationship with a Global Payments' Organisation. 
 


**Customer Statuses**

***Status*** | ***Description***
-------------- | -------------- 
ACTIVE | This indicates that a Customer is active and can be used to process real transactions with.
DISABLED | This indicates that a Customer can no longer be used for payment processing. The Customer resource is never deleted to maintain integrity and a record of historical activity. 

**Customer  Requests**

### *create*
Used to create a new Customer on Global Payments' system

### *read*
Used to retrieve information about an existing Customer.

### *update*
Used to update information about an existing Customer.



## Payment Method

A payment instrument own by the Customer used in transactions to Global Payments for the purposes of Sale and Refund Transactions.


**Payment Method Types**

***Type*** | ***Description***
-------------- | -------------- 
 CARD | The payment instrument is a Customer's debit or credit card where a PAN and expiry date are stored securely by Global Payments.
 BANK ACCOUNT | The payment instrument is a Customer's bank account based payment method where a sort code/routing number and bank account number are stored securely by Global Payments.
 


**Payment Method Statuses**

***Status*** | ***Description***
-------------- | -------------- 
ACTIVE | This indicates that the Payment Method is active and can be used to process real transactions with.
DISABLED | This indicates that the Payment Method can no longer be used for payment processing. 

**Payment Method Requests**

### *create*
Used to create a new Payment Method on the Global Payments' system

### *read*
Used to retrieve information about an existing Payment Method.

### *update*
Used to update information about an existing Payment Method.




## Order

An Order is representation of an amount owed by a Customer to a Merchant. It has an amount and currency. An Order may be associated with multiple Transactions.


**Order Types**

***Type*** | ***Description***
-------------- | -------------- 
 STANDALONE | A once off standalone Order.
 RECURRING | An Order that requires a sequence of scheduled transactions to complete successfully, dictated by a Global Payments' Payment Schedule.
 


**Order Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 OPEN | The Order is still open and not yet fulfilled. One or more transactions may have been executed to fulfill the Order but the amount has not been wholly or partially fulfilled.
 FULFILLED | The amount has been fulfilled with one or more transactions.
 CLOSED | The Order has been closed due to the Order expiring before the Order is fulfilled or the Order being specifically closed by the Organisation.


**Order  Requests**

### *create*
Used to create a new Order on the Global Payments' system

### *read*
Used to retrieve information about an existing Order.

### *update*
Used to update information about an existing Order.


## Payment Schedule

A schedule of Transactions or Orders that need to be fulfilled.


**Payment Schedule Types**

***Type*** | ***Description***
-------------- | -------------- 
 SUBSCRIPTION | Paying a regular amount at specific intervals.
 INSTALLMENT | Paying an amount at regular intervals to pay back a total amount.
 


**Payment Schedule Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 OPEN | The Order is still open and not yet fulfilled. One or more transactions may have been executed to fulfill the Order but the amount has not been wholly or partially fulfilled.
 FULFILLED | The amount has been fulfilled with one or more transactions.
 CLOSED | The Order has been closed due to the Order expiring before the Order is fulfilled or the Order being specifically closed by the Organisation.


**Payment Schedule Requests**

### *create* 
Used to create a new Order on the Global Payments' system

### *read* 
Used to retrieve information about an existing Order.

### *update* 
Used to update information about an existing Order.


# Version

## Get All Report OBs

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
api.r_eng.get
```



```pythonimport gp_rep

api = gp_rep.authorize('success')
api.r_eng.get()
```

```shell
curl "http://example.com/api/r_eng"
  -H "Authorization: success"
```

```javascript
const gp_rep = require('gp_rep');

let api = gp_rep.authorize('success');
let r_eng = api.r_eng.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "batch": "Fluffums",
    "date": "12/01/2017",
    "fee1": 6,
    "deduction1": -2
  },
  {
    "id": 2,
    "batch": "Fluffums",
    "date": "12/01/2017",
    "fee1": 6,
    "deduction1": -2
  },
]
```

This endpoint retrieves all report objects.

### HTTP Request

`GET http://example.com/api/report1234`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include r_eng that have already been adopted.

<aside class="success">
Remember — authentication is key!
</aside>

## Get a Specific key

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
api.r_eng.get(2)
```

```python
import gp_rep

api = gp_rep.authorize('success')
api.r_eng.get(2)
```

```shell
curl "http://example.com/api/r_eng/2"
  -H "Authorization: success"
```

```javascript
const gp_rep = require('gp_rep');

let api = gp_rep.authorize('success');
let max = api.r_eng.get(2);
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "batch": "Fluffums",
    "date": "12/01/2017",
    "fee1": 6,
    "deduction1": -2
  }
```

This endpoint retrieves a specific key.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/r_eng/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the key to retrieve

## Delete a Specific key

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
api.r_eng.delete(2)
```

```python
import gp_rep

api = gp_rep.authorize('success')
api.r_eng.delete(2)
```

```shell
curl "http://example.com/api/r_eng/2"
  -X DELETE
  -H "Authorization: success"
```

```javascript
const gp_rep = require('gp_rep');

let api = gp_rep.authorize('success');
let max = api.r_eng.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific key.

### HTTP Request

`DELETE http://example.com/r_eng/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the key to delete

