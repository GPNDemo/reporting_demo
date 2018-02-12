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

# Resources
Resources ensure there is a common understanding of our product throughout our organisation and a common terminology when we communicate internally and to the market.  Resources inform the features we need to build to solve our customers’ problems.

Resources can have a **Status**, a **Type**, **Data** and **Relationships** to other resources. 

**Requests** are actions that are taken to affect Resources.

Each instance of a Resource has a unique **Global Payments ID**. This is a Global Payments reference that uniquely identifies the resource on the Global Payments system.

----------------------------------------------------------------------------------------------------------------

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

### create
Used to create a new Organisation on Global Payments' system.

### read
Used to retrieve information about an existing Organisation.

### update
Used to update information about an existing Organisation.

----------------------------------------------------------------------------------------------------------------

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

### create
Used to create a new Account on Global Payments' system

### read
Used to retrieve information about an existing Account.

### update
Used to update information about an existing Account.

----------------------------------------------------------------------------------------------------------------

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
 PREAUTHORISED | 
 OPEN_BATCH | 
 VOIDED | 
 BATCHED |
 DEPOSITED |
 DISPUTED |
 DECLINED | 
 ERROR |  

**Transaction Requests**

### authorise
Organisation initiated request to Authorise a transaction. If authorised successfully and flagged for auto-capture then the transaction would be have an OPEN-BATCH Status.  If successfully authorised and not flagged for auto-capture then the transaction would be have a PREAUTHORISED Status. A separate capture request is needed to move the transactions from a PREAUTHORISED status to an OPEN-BATCH status.

### cancel
Organisation initiated request to void a transaction. This can be applied to successful authorised/preauthorised transactions and stops the transaction from going further in its' lifecycle.
This request must be executed before the Transaction has a status of BATCHED

### refund
Organisation initiated request to Refund a Customer money. This can be linked to an previous Payment transaction or a standalone where it does not link to a previous Payment Transaction.

### adjust
Organisation initiated request to change the amount of a transaction that has a status of PREAUTHORISED or OPEN-BATCH. e.g. to add a tip.
This request must be executed before the Transaction has a status of BATCHED

### capture
Organisation initiated request to start the process of moving funds between the Customer and the Organisation. It changes a transaction with a status of PREAUTHORISED to have a status of OPEN-BATCH. 

### hold
This is an organisation initiated request which If a transaction has an Open Batch status then putting it on hold removes it from the Open Batch but does not void the transaction. This could be used to pause a transaction for being processed in a Batch to check inventory or do fraud analysis

### release
If a Transaction has a current status of HELD then a release request will re-assign it a status of Open-Batch

### force
This is a request initiated by an Organisation that puts a transaction directly into an Open-Batch status and does not request an Authorisation/PreAuthorisation via the processor as the authcode has been attained elsewhere.

### close-batch
Where does this sit?

### read
Used to retrieve information about an existing Transaction.

### update
Used to update information about an existing Transaction. Can this incorporate adjust, cancel, hold, release?


----------------------------------------------------------------------------------------------------------------

## Deposit

The initiation of a Debit or a Credit to a Merchant's Bank Account that relates to Transactions and Disputes processed via Global Payments or fees charged by Global Payments to the Organisation. 

**Deposit Types**

***Type*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**Deposit Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 DELAYED | 
 RESERVED | 
 DEPOSITED | 
 


**Deposit  Requests**

### action1
### action2
### action3

----------------------------------------------------------------------------------------------------------------

## Dispute

An act, initiated by the Customer or their bank, to challenge a previous transaction with a view to getting more information about that transaction or reversing the transfer of funds between that Customer and the Merchant for that transaction.

**Dispute Types**

***Type*** | ***Description***
-------------- | -------------- 
 INQUIRY | 
 CHARGEBACK | 
 REPRESENTMENT |  

**Dispute Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 OPEN | 
 PENDING | 
 CLOSED | 


**Dispute  Requests**

### notify
### challenge
### read
### accept
### update

----------------------------------------------------------------------------------------------------------------

## RESOURCE1

Resource Description here


**RESOURCE1 Types**

***Type*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1 Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1  Requests**

### action1
### action2
### action3


----------------------------------------------------------------------------------------------------------------

## RESOURCE1

Resource Description here


**RESOURCE1 Types**

***Type*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1 Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1  Requests**

### action1
### action2
### action3


----------------------------------------------------------------------------------------------------------------

## RESOURCE1

Resource Description here


**RESOURCE1 Types**

***Type*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1 Statuses**

***Status*** | ***Description***
-------------- | -------------- 
 | 
 | 
 | 


**RESOURCE1  Requests**

### action1
### action2
### action3


----------------------------------------------------------------------------------------------------------------

















# Version

## Get All Report OBs

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
api.r_eng.get
```

```python
import gp_rep

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

