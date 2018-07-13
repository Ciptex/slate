---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - Node.js

toc_footers:
  - <a href='#'></a>
  - <a href='#'>Documentation Powered by Ciptex</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Hermes API.

In this document you will find essential API calls you need to get up and start with your deploymnet.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```Node.js
```

> Make sure to replace `{bearer_token}` with your API key.

Authenticate the user with the system and obtain the auth_token

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer {bearer_token}`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Hermes

## Get Agents

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "Sod-FHwK", "createat": "2018-01-31T11:20:21Z", "updateat": "2018-01-10T17:29:03Z", "firstname": "Agent", "lastname": "Test", "agentid": 1000 }]
```

This endpoint retrieves all Agents.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Break Codes

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SogrYcgK", "createat": "2017-05-31T14:25:12Z", "updateat": "2017-05-31T14:25:12Z", "description": "Break AM", "allowedtime": 10, "pausecodeid": 0, "groupname": "Standard" }] 
```

This endpoint retrieves all Break Codes.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Email Campaigns

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SozCIXUK", "createat": "2018-06-01T11:18:16Z", "updateat": "2018-06-07T09:03:25Z", "description": "Test", "queueid": 0, "openingid": "35F64636424415B4", "holidayid": "35F64692456437B4", "statusgroup": 1, "priority": 0, "phonedisplayspecific": "01613750777", "mediatype": "Email", "campaignid": "35F6A734538555B4", "scriptid": 0, "scriptname": "", "email": "", "replayemail": "" }]
```

This endpoint retrieves all Email Campaigns.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Inbound Campaigns

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "Sov1lLcK", "createat": "2018-06-01T07:41:09Z", "updateat": "2018-07-09T09:57:03Z", "description": "TEST", "queueid": 100, "openingid": "35F64636424415B4", "holidayid": "", "statusgroup": 3, "deflanguage": "EN", "priority": 80, "phonedisplayspecific": "01613750777", "mediatype": "Telephony", "campaignid": "221050", "scriptid": 26, "scriptname": "Test", "voicescriptname": "", "endvoicescriptname": "", "clienthoursoid": "SodGwBcK" }]
```

This endpoint retrieves all Inbound Campaigns.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>


## Get Manual Campaigns

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "Sow3gWsK", "createat": "2018-06-01T11:06:56Z", "updateat": "2018-06-06T12:16:09Z", "description": "Test", "openingid": "", "holidayid": "", "statusgroup": 1, "deflanguage": "EN", "phonedisplayspecific": "01613750777", "mediatype": "Telephony", "campaignid": "35F69738717537B4", "scriptid": 23, "scriptname": "Test" }]
```

This endpoint retrieves all Manual Campaigns.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>


## Get Outbound Campaigns

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SqeGfBsK", "createat": "2018-06-06T13:21:19Z", "updateat": "2018-06-07T09:04:13Z", "description": "Test", "openingid": "", "holidayid": "", "statusgroup": -1, "deflanguage": "EN", "phonedisplayspecific": "01613750777", "mediatype": "Telephony", "campaignid": "35175645615437B4", "scriptid": -1, "scriptname": "", "endvoicescriptname": "", "clienthoursoid": "", "outmode": "Preview" }]
```

This endpoint retrieves all Outbound Campaigns.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>


## Get Customer Hours

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SodBRBQK", "createat": "2018-05-31T10:19:45Z", "updateat": "2018-05-31T10:21:03Z", "description": "Test", "openinghour": [   { "begin": 480, "end": 1200 },   { "begin": 1920, "end": 2640 },   { "begin": 3360, "end": 4080 },   { "begin": 4800, "end": 5520 },   { "begin": 6240, "end": 6960 },   { "begin": 7680, "end": 8220 } ] 
```

This endpoint retrieves all Customer Hours.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Disposition Groups

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SogsrdsK", "createat": "2018-05-31T14:26:35Z", "updateat": "2018-05-31T14:26:43Z", "description": "Test", "currency": "£", "statusgroupid": 1 }]
```

This endpoint retrieves all Disposition Groups.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Dispositions

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SoguweEK", "createat": "2018-05-31T14:29:52Z", "updateat": "2018-05-31T14:29:52Z", "description": "Test", "statusgroupid": 1, "statuscode": 1, "statusdetailed": 0, "positive": false, "argued": false, "nonargued": false, "cost": 0, "validquota": false }] 
```

This endpoint retrieves all Dispositions.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Holiday Groups

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SodYDDsK", "createat": "2018-05-31T10:39:47Z", "updateat": "2018-06-06T13:10:12Z", "description": "Default Holidays", "timezoneid": "GMT Standard Time", "holidaygroupid": "35F61735444437B4", "holidayitems": [   { "oid": "SodYODwK", "description": "Bank holiday", "closedday": 7, "closedmonth": 5, "closedyear": 0, "message": "\\10.255.0.135\acd_c\hermes_p\Files\35F6B4653464D4B4\recep t\221050\BankHoliday.wav", "hourbegin": 0, "hourend": 2359, "holidayitemid": 1 }] }] 
```

This endpoint retrieves all Holiday Groups.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Queues 

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SodB5B4W", "createat": "2018-05-31T10:25:45Z", "updateat": "2018-05-31T10:25:45Z", "description": "TEST", "queueid": 100 }]
```

This endpoint retrieves all Queues.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Service Hours

```Node.js
```

> The above command returns JSON structured like this:

```json
[{ "oid": "SodW4DEK", "createat": "2018-05-31T10:32:08Z", "updateat": "2018-05-31T10:32:41Z", "description": "Standard Hours", "timezoneid": "GMT Standard Time", "servicehoursgroupid": "35F62665434454B4", "openinghour": [   { "begin": 480, "end": 1200 },   { "begin": 1920, "end": 2640 },   { "begin": 3360, "end": 4080 },   { "begin": 4800, "end": 5520 },   { "begin": 6240, "end": 6960 },   { "begin": 7740, "end": 7920 } ], }] 
```

This endpoint retrieves all Service Hours.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>

## Get Supervisor Groups

```Node.js
```

> The above command returns JSON structured like this:

```json
{ "oid": "SoKFGUUK", "createat": "2018-05-30T12:42:26Z", "updateat": "2018-07-10T11:21:44Z", "description": "default group", "supervisegroupid": 0, "agents": [1000,1001,1002]
```

This endpoint retrieves all Supervisor Groups.

### HTTP Request

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups`

### Query Parameters

<aside class="success">
200 HTTP Status Code
</aside>