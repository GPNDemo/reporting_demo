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

## Organisation

Organisations are typically businesses that have a contracted with Global Payments. Global Payments provides payment processing solutions to Organisations. Organisations can be Merchants, ISO, ISVs, VARs or Marketplaces. Organisations can be owned by Global Payments.

A **Merchant** Organisation which has a contractual relationship with Global Payments for the provision of financial payment services, and/or technical payment services.  

A **Marketplace** Organisation which has a contractual relationship with Global Payments to resell or refer Global Payments' services.
Merchants contract with Marketplaces 

An **ISO** Organisation which has a contractual relationship with Global Payments to resell or refer Global Payments' services.
Merchants contract with ISOs.

**Organisation Statuses**
***Status*** | *Description*| 
-------------- | -------------- 
CREATED | This indicates that an Organisation or an Account has been created. 
ACTIVE LIVE | This indicates that an Organisation or an Account is in live mode can can be used to process real transactions.
ACTIVE TEST | This indicates that an Organisation or an Account is it test mode and that any activity against the Organisatin or Account will never result in real payment processing,
 DISABLED | This indicates that the Organisation or an Account can no longer be used for payment processing. These resources are never deleted to maintain integrity and a record of historical activity. A reason would be associated with the disabling of an Organisation or an Account
ERROR | Indicating that an Organisation or Account was not successfully created or updated. This could be incomplete application or concerns due to credit & risk or information missing resulting in an incomplete application.


 
### create
### read
### update

## Account

A representation of a data needed to configure an Organisation to process payments. Typically this would information such as Organisation Deposit Bank Accounts, Allowed Functionality for that Account, Payment Method Specific details e.g. For Cards it would be the MID and TID.

### create
Used to create a new Organisation or Account on Global Payments' system

### read
Used to retrieve information about an existing Organisation or Account.

### update
Used to update information about an existing Organisation or Account.


## Transaction

An act to attempt the transfer of funds between the Customer and the Merchant

A Payment is a transaction between a Customer and a Merchant in which the transfer of funds goes from the former to the latter

A Refund is a transaction between a Customer and a Merchant in which the transfer of funds goes from the latter to the former

### authorise
### preauthorise
### cancel
### refund
### adjust
### batch
### hold
### release
### force
### read
### edit

## Deposit

The initiation of a Debit or a Credit to a Merchant's Bank Account relating to the Sale and Refund Transactions processed via the Techncial and Financial services provided by the Payment Processor.

## Dispute

An act, initiated by the Customer or their bank, to challenge a previous transaction with a view to getting more information or reversing the transfer of funds between that Customer and the Merchant for that transaction.

### notify
### challenge
### read
### accept


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

