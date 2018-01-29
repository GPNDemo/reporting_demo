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
  - Globalpayments Powering Insights
  - <a href='https://www.globalpaymentsinc.com'>www.globalpaymentsinc.com</a>

includes:
  - errors

search: true
---

# Resources

Resources ensure there is a common understanding of our product throughout our organisation and a common terminology when we communicate internally and to the market.  Resources inform the features we need to build to solve our customers’ problems.

Resources have a Status, Type, Data and Relationships to other entities. 

Requests are actions that are taken to affect Resources.

Each instance of a Resource has a unique GPN generated ID. 


## Organisation

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
```

```python
import gp_rep

api = gp_rep.authorize('success')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: success"
```

```javascript
const gp_rep = require('gp_rep');

let api = gp_rep.authorize('success');
```

> Make sure to replace `success` with your API key.

Organisations are typically businesses that have a contracted with GPN. GPN provides payment processing solutions to Organisations. Organisations can be Merchants, ISO, ISVs, VARs or Marketplaces. Organisations can be owned by GPN.

A Merchant Organisaion which has a contractual relationship with a processor for the provision of financial payment services, and/or technical payment services.  

A Marketplace Organisation which has a contractual relationship with a Processor to resell or refer a Processor's financial payment services and/or technical payment services.
Merchants contract with Marketplaces 

An ISO Organisation which has a contractual relationship with a Processor to resell or refer a Processor's financial payment services and/or technical payment services.
Merchants contract with ISOs



> To authorize, use this code:

```ruby
require 'gp_rep'

api = gp_rep::APIClient.authorize!('success')
```

```python
import gp_rep

api = gp_rep.authorize('success')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: success"
```

```javascript
const gp_rep = require('gp_rep');

let api = gp_rep.authorize('success');
```

> Make sure to replace `success` with your API key.

### new
### read
### edit
### disable

## Transaction

An act to attempt the transfer of funds between the Customer and the Merchant

A Payment is a transaction between a Customer and a Merchant in which the transfer of funds goes from the former to the latter

A Refund is a transaction between a Customer and a Merchant in which the transfer of funds goes from the latter to the former

### authorise
### preauthorised
### cancel
### refund
### return
### batch
### read
### hold
### release
### adjust
### force
### edit

## Deposit

The initation of a Debit or a Credit to a Merchant's Bank Account relating to the Sale and Refund Transactions processed via the Techncial and Financial services provided by the Payment Processor.

## Dispute

An act, initiated by the Customer to challenge and reverse the transfer of funds between that Customer and the Merchant


### notify
### challenge
### read
### edit
### resolve 


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

