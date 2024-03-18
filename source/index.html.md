---
title: OpiGo API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#' onclick="alert('Comming soon!');">Request for Key and Secretxs</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the OpiGo API
---

# Introduction

Welcome to the OpiGo API! You can use our API to access Marketplace API endpoints, which can get information on various cards like returns and so on.

We have language bindings in Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Base URL

https://staging.opigo.co.in/marketplace


# Authentication

## Authenticate test examples

OpiGo uses API key and secret to allow access to the API. You can request OpiGo to get your personal key and secret.

<strong>key</strong>: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
<br>
<strong>secret</strong>: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

<aside class="notice">
You must replace <code>key and secret</code> with your personal API key and secret.
</aside>

> To authorize, use this code:

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/cards/get_cards", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
{"message": "success", "status": 200, "code": 200}
```

```python
# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/data/test"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')

const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";


const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/data/test",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint to test your implementation is working or not.

### HTTP Request

`POST base_url + /api/v1/data/test`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty

<aside class="success">
Remember — Please remember to send timestamp
</aside>

# Channels

## Get All Channels

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i,
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/data/channels", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"id": "158760cf-2bba-4be4-b0f2-fd2bdc221c3e", "title": "General", "description": "This is general channel", "status": "active", "created_at": "2023-10-10T14:16:34.866+05:30", "updated_at": "2023-10-10T14:16:34.866+05:30", "subscriptions": [{"id": "0e50508a-ae23-40ae-8773-c1f833e1f6dc", "title": "General", "description": "", "channel_id": "158760cf-2bba-4be4-b0f2-fd2bdc221c3e", "num_of_cards": 5, "price": "20.7", "status": "active", "created_at": "2023-10-10T14:16:47.936+05:30", "updated_at": "2024-01-17T14:16:51.506+05:30"}]}, {"id": "df11f3a5-da5c-4fcc-b00b-4ffbcb029bc4", "title": "Long Term", "description": "this is long term channel", "status": "active", "created_at": "2023-10-10T16:21:53.480+05:30", "updated_at": "2023-10-10T16:21:53.480+05:30", "subscriptions": [{"id": "bcd9afe6-7aa7-4420-828e-796d06c6a550", "title": "Long Term", "description": "this is just a test", "channel_id": "df11f3a5-da5c-4fcc-b00b-4ffbcb029bc4", "num_of_cards": 10, "price": "1.0", "status": "active", "created_at": "2023-10-10T16:22:17.528+05:30", "updated_at": "2024-01-26T12:27:03.744+05:30"}]}, {"id": "0c3248b8-2d7d-4b90-851a-686197a01efd", "title": "Medium Term", "description": "Medium Term", "status": "active", "created_at": "2023-12-07T08:16:32.449+05:30", "updated_at": "2023-12-07T08:16:32.449+05:30", "subscriptions": [{"id": "ad8fa9b0-722b-43f9-a6df-69e4e0cc1761", "title": "Medium Term", "description": "Medium Term", "channel_id": "0c3248b8-2d7d-4b90-851a-686197a01efd", "num_of_cards": 10, "price": "500.0", "status": "active", "created_at": "2024-01-10T17:35:57.727+05:30", "updated_at": "2024-01-10T17:35:57.727+05:30"}]}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/data/channels"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')

const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";


const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/data/channels",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves all channels.

### HTTP Request

`POST base_url + /api/v1/data/channels`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty

<aside class="success">
Remember — Please remember to send timestamp
</aside>


# Channel Cards

## Get All Cards

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i,
  "channels": "General,Medium Term"
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/cards/get_cards", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"expert_full_name": "Sandeep Maurya", "caption": "", "expert_view": "Bullish", "timeframe": "Next 1 Week", "potential_range": "Between 5% - 10%", "stock_name": "HDFCAMC - HDFCSENSEX", "symbol_name": "HDFCSENSEX", "cost_price": "714.51", "currency": "INR", "card_status": "closed", "overdue_status": false, "ltp": "777.0", "ltp_timestamp": 0, "stock_split_id": null, "highest_price_achieved": "0.0", "target_range_price": "750.24", "target_achieved_timestamp": 0, "pnl": "62.49", "pnl_percentage": "8.74585", "closing_price": "777.0", "closing_price_timestamp": 1704977779000, "creation_timestamp": 1704961716000, "updation_timestamp": 1704977779000}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/cards/get_cards"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')

const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/cards/get_cards",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves all cards.

### HTTP Request

`POST base_url + /api/v1/cards/get_cards`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty
channels  | No.  | comma(,) seperated channels for ex channels: "General,Medium Term"

<aside class="success">
Remember — Please remember to send timestamp
</aside>



## Get specific card

<aside class="success">
comming soon
</aside>


# Public Cards

## Get All Cards

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i,
  "channels": "General,Medium Term"
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/public/cards/get_cards", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"expert_full_name": "Sandeep Maurya", "caption": "", "expert_view": "Bullish", "timeframe": "Next 1 Week", "potential_range": "Between 5% - 10%", "stock_name": "HDFCAMC - HDFCSENSEX", "symbol_name": "HDFCSENSEX", "cost_price": "714.51", "currency": "INR", "card_status": "closed", "overdue_status": false, "ltp": "777.0", "ltp_timestamp": 0, "stock_split_id": null, "highest_price_achieved": "0.0", "target_range_price": "750.24", "target_achieved_timestamp": 0, "pnl": "62.49", "pnl_percentage": "8.74585", "closing_price": "777.0", "closing_price_timestamp": 1704977779000, "creation_timestamp": 1704961716000, "updation_timestamp": 1704977779000}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/public/cards/get_cards"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')


const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/public/cards/get_cards",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves all cards.

### HTTP Request

`POST base_url + /api/v1/public/cards/get_cards`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty
channels  | No.  | comma(,) seperated channels for ex channels: "General,Medium Term"

<aside class="success">
Remember — Please remember to send timestamp
</aside>

---------------------
# General Informations

## Get Polls

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i,
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/data/polls", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"account_id": 192, "account_name": "Devansh Mehta", "title": "Poll Title", "description": "", "status": "finished", "schedule": null, "approved_at": null, "view_count": null, "answer_count": null, "poll_type": "single_investment", "poll_category_id": 2, "time_frame": "next_1_month", "data": {"investment_type": "new_investment", "vote_options": ["bullish", "bearish", "neutral"]}, "question": null, "stock_name": [], "final_response": {"bullish": 100, "bearish": 0, "neutral": 0}, "new_final_response": [{"bullish": 100}, {"bearish": 0}, {"neutral": 0}], "verified_opigo_expert_response": [], "total_comment_count": null, "created_at": "2023-08-04T21:35:36.526+05:30", "updated_at": "2023-08-04T22:45:14.714+05:30"}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/data/polls"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')


const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/data/polls",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves all cards.

### HTTP Request

`POST base_url + /api/v1/data/polls`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty

<aside class="success">
Remember — Please remember to send timestamp
</aside>



## Get Posts

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i,
  "channels": "General,Medium Term"
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/data/posts", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"category": "video", "category_id": 2, "account_id": 205, "account_name": "Sandeep Maurya", "caption": "Which stock did you start with in 2024? I began with Dredging Corp of India 🚀", "is_complete": false, "resize_mode": null, "total_comment_count": null, "created_at": "2024-01-09T15:53:23.158+05:30", "updated_at": "2024-01-09T15:53:23.158+05:30"}, {"category": "video", "category_id": 2, "account_id": 205, "account_name": "Sandeep Maurya", "caption": "This just a test", "is_complete": false, "resize_mode": null, "total_comment_count": null, "created_at": "2023-09-29T12:40:40.215+05:30", "updated_at": "2023-09-29T12:40:40.215+05:30"}, {"category": "video", "category_id": 2, "account_id": 203, "account_name": "Jzns Hwnz", "caption": "", "is_complete": false, "resize_mode": "", "total_comment_count": null, "created_at": "2023-09-08T11:07:55.413+05:30", "updated_at": "2023-09-08T11:07:55.413+05:30"}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/data/posts"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')


const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/data/posts",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves all cards.

### HTTP Request

`POST base_url + /api/v1/data/posts`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty

<aside class="success">
Remember — Please remember to send timestamp
</aside>

# Stocks

## Get Trending Stocks

```ruby

require 'json'
require 'http'
require 'openssl'

secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"

payload = {
  "timestamp": Time.new.to_i
}

signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), secret, payload.to_json)

response = HTTP.headers("Content-Type"=> "Application/json", "X-AUTH-APIKEY" => key, "X-AUTH-SIGNATURE" => signature).post("#{base_url}/api/v1/data/trending_stocks", json: payload)

response_body = JSON.parse response.body
```

> The above command returns JSON structured like this:

```json
[{"expert_full_name": "Sandeep Maurya", "caption": "", "expert_view": "Bullish", "timeframe": "Next 1 Week", "potential_range": "Between 5% - 10%", "stock_name": "HDFCAMC - HDFCSENSEX", "symbol_name": "HDFCSENSEX", "cost_price": "714.51", "currency": "INR", "card_status": "closed", "overdue_status": false, "ltp": "777.0", "ltp_timestamp": 0, "stock_split_id": null, "highest_price_achieved": "0.0", "target_range_price": "750.24", "target_achieved_timestamp": 0, "pnl": "62.49", "pnl_percentage": "8.74585", "closing_price": "777.0", "closing_price_timestamp": 1704977779000, "creation_timestamp": 1704961716000, "updation_timestamp": 1704977779000}]
```

```python

# python3

import hmac
import hashlib
import base64
import json
import time
import requests

key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
base_url = "https://staging.opigo.co.in/marketplace"


secret_bytes = bytes(secret, encoding='utf-8')

timeStamp = int(round(time.time() * 1000))

body = {
  "timestamp": timeStamp
}

json_body = json.dumps(body, separators = (',', ':'))

signature = hmac.new(secret_bytes, json_body.encode(), hashlib.sha256).hexdigest()

url = base_url + "/api/v1/data/trending_stocks"

headers = {
    'Content-Type': 'application/json',
    'X-AUTH-APIKEY': key,
    'X-AUTH-SIGNATURE': signature
}

response = requests.post(url, data = json_body, headers = headers)
data = response.json()
print(data)
```

```javascript

const request = require('request')
const crypto = require('crypto')


const key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const secret = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
const base_url = "https://staging.opigo.co.in/marketplace"

const timeStamp = Math.floor(Date.now());

const body = {
  "timestamp": timeStamp
}

const payload = new Buffer(JSON.stringify(body)).toString();
const signature = crypto.createHmac('sha256', secret).update(payload).digest('hex')

const options = {
  url: base_url + "/api/v1/data/trending_stocks",
  headers: {
      'X-AUTH-APIKEY': key,
      'X-AUTH-SIGNATURE': signature
  },
  json: true,
  body: body
}

request.post(options, function(error, response, body) {
  console.log(body);
});
```

This endpoint retrieves trending stocks.

### HTTP Request

`POST base_url + /api/v1/data/trending_stocks`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
timestamp | true | You can't send the body empty

<aside class="success">
Remember — Please remember to send timestamp
</aside>
---------------------

# Errors

Code | Meaning
-----|  -------
400  | Bad Request -- Your request is invalid.
401  | Unauthorized -- Invalid Authorization X-AUTH-APIKEY or API Key and Secret is not active.
422  | Invalid Request - Invalid Request Either data tempered or invalid signature or Subscription has been expired.
404  | Not Found -- The specified link could not be found.
429  | Too Many Requests -- You're making too many API calls
500  | Internal Server Error -- We had a problem with our server. Try again later.
503  | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
