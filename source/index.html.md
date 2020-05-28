---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Candide Garden API. You can use our API to access Garden API endpoints, which can get information on your Tickets and Checkins.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://garden-api.candideapp.com"
  -H "Authorization: plants-plants-plants"
```

> Make sure to replace `plants-plants-plants` with your API key.

Candide Garden API uses API keys to allow access to the API. You can register a new API key at our [CMS](https://cms.candideapp.com/api-keys).

The Garden API expects the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: plants-plants-plants`

<aside class="notice">
You must replace <code>plants-plants-plants</code> with your personal API key.
</aside>

# Tickets

## Get All Tickets

```shell
curl "https://garden-api.candideapp.com/tickets"
  -H "Authorization: plants-plants-plants"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "10715970-8aa8-4a54-9d74-c5dc6738364f",
    "candideUser": true,
    "expiresAt": "2022-02-20T23:59:59.000Z",
    "startsAt": "2021-02-21T00:00:00.000Z",
    "createdAt": "2020-03-18T15:28:01.778Z",
    "paymentStatus": null,
    "paymentIntentId": null,
    "email": "th111@whatever.com",
    "preferences": {
      "canEmail": false,
      "canPhone": true
    },
    "phone": "+441111111552",
    "productName": "Garden Membership",
    "visitors": {
      "Child": 1,
      "Adult": 1
    },
    "fullAddress": "1, Street Way, Road St",
    "status": "ACTIVE"
  },
  {
    "id": "9abf5e8a-74dd-441d-a3a0-2c21fe608bb2",
    "candideUser": true,
    "expiresAt": "2021-02-20T23:59:59.000Z",
    "startsAt": "2020-02-21T00:00:00.000Z",
    "createdAt": "2020-02-21T14:41:13.768Z",
    "paymentStatus": null,
    "paymentIntentId": null,
    "email": "th111@whatever.com",
    "preferences": {
      "canEmail": false,
      "canPhone": true
    },
    "phone": "+441111111552",
    "productName": "Garden Membership",
    "visitors": {
      "Adult": 1,
      "Child": 1
    },
    "fullAddress": "1, Street Way, Road St",
    "status": "ACTIVE"
  }
]
```

This endpoint retrieves all tickets.

### HTTP Request

`https://garden-api.candideapp.com/tickets`

### Query Parameters

| Parameter | Default | Description                                                                          |
| --------- | ------- | ------------------------------------------------------------------------------------ |
| startDate |         | Filter out all records before this date and time. ISO Format YYYY-MM-DDTHH:mm:ss UTC |
| endDate   | now     | Filter out all records after this date and time                                      |
| after     |         | The id of the last record from the previous page                                     |
| limit     | 10      | The number of records per page                                                       |
| sortOrder | ASC     | ASC or DESC                                                                          |

# Check-ins

## Get All Check-ins

```shell
curl "https://garden-api.candideapp.com/checkins"
  -H "Authorization: plants-plants-plants"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "61515eb4-10f7-4eed-b835-5fe385cf53cd",
    "checkinTime": "2020-04-27T16:30:41.023Z",
    "notes": null,
    "ticketId": "e4213f17-3631-4f3d-98a5-f1c8b57e0159",
    "attendance": {
      "Adult": 1
    },
    "email": "th111@whatever.com",
    "phone": "01445 326598"
  },
  {
    "id": "55c77fe7-4885-4a7a-a554-cdf9649f74d0",
    "checkinTime": "2020-04-27T16:22:09.674Z",
    "notes": null,
    "ticketId": "e4213f17-3631-4f3d-98a5-f1c8b57e0159",
    "attendance": {
      "Adult": 1
    },
    "email": "th111@whatever.com",
    "phone": "01445 326598"
  }
]
```

This endpoint retrieves all check-ins.

### HTTP Request

`https://garden-api.candideapp.com/checkins`

### Query Parameters

| Parameter | Default | Description                                                                          |
| --------- | ------- | ------------------------------------------------------------------------------------ |
| startDate |         | Filter out all records before this date and time. ISO Format YYYY-MM-DDTHH:mm:ss UTC |
| endDate   | now     | Filter out all records after this date and time                                      |
| ticketId  |         | Return only checkins for the specified ticket                                        |
| after     |         | The id of the last record from the previous page                                     |
| limit     | 10      | The number of records per page                                                       |
| sortOrder | ASC     | ASC or DESC                                                                          |
