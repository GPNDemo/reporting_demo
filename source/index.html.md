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

# Reporting API

Sometimes there is need for more specialized reporting, beyond what is available in the Dashboard.

Globalpayments Reporting API gathers transaction data from start to finish, enabling you to gain valuable insights anywhere along the chain.

The API is designed to be as flexible as possible. Our engine takes on all the heavy lifting in the backend. 
You can create your own reporting tool and access all of your account information using the API. Our API returns data in the JSON format, allowing you the ability to slot your new data stream directly into your existing workflow - quickly and easily.

This API reference outlines the expected requests and responses to use GlobalPayments Reporting API.

## Getting started

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

Reporting API provides a number of ways of connecting and formatting requests, so you can choose what works best for your platform.

Choose your flavor from the tabs on the code pane. We have a wide selection of JSON wrappers for all popular languages.

REST (JSON) - recommended
SOAP
cURL
PHP
This reference focusses on REST using JSON and SOAP in examples. The other interfaces follow the same structure and the endpoints are provided for each.



# Authentication

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

gp_rep uses API keys to allow access to the API. You can register a new gp_rep API key at our [developer portal](http://example.com/developers).

gp_rep expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: success`

<aside class="notice">
You must replace <code>success</code> with your personal API key.
</aside>

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

