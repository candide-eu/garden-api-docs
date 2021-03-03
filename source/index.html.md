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
{
  "tickets": {
    "results": [
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
        "visitorTypes": [
          {
            "id": "4356b3a9-1d7b-4449-a6ce-10ff6d2ba85f",
            "name": "Adult",
            "isChild": false
          },
          {
            "id": "2943ee0b-081f-4f77-a766-8e263dcdb442",
            "name": "Child",
            "isChild": true
          }
        ],
        "fullAddress": "1, Street Way, Road St",
        "status": "ACTIVE",
        "holderFirstName": "Test",
        "holderLastName": "Person",
        "markedForDeletion": false
      },
      ...
    ],
    "backwardEdge": "id:10715970-8aa8-4a54-9d74-c5dc6738364f,createdAt:1591369643939",
    "forwardEdge": "id:9abf5e8a-74dd-441d-a3a0-2c21fe608bb2,createdAt:1591365113606",
    "hasMore": true,
    "numberOfAllItems": 4019,
    "numberOfPageItems": 1
  }
}
```

This endpoint retrieves all tickets.

<aside class="notice">
Please note that a ticket which is <code>markedForDeletion</code> will be deleted from the system on the <code>expiresAt</code> date.

To remain compliant with GDPR regulations, please delete from any records you keep on this date.
</aside>

### HTTP Request

`https://garden-api.candideapp.com/tickets`

### Query Parameters

| Parameter | Default | Description                                                                          |
| --------- | ------- | ------------------------------------------------------------------------------------ |
| startDate |         | Filter out all records before this date and time. ISO Format YYYY-MM-DDTHH:mm:ss UTC |
| endDate   | now     | Filter out all records after this date and time                                      |
| after     |         | A cursor from the previous page. Use forwardEdge and backwardEdge to traverse pages  |
| limit     | 10      | The number of records per page                                                       |
| sortOrder | ASC     | ASC or DESC                                                                          |

## Get All Updated Tickets

```shell
curl "https://garden-api.candideapp.com/ticket-updates"
  -H "Authorization: plants-plants-plants"
```

> The above command returns JSON structured like this:

```json
{
  "tickets": {
    "results": [
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
        "visitorTypes": [
          {
            "id": "4356b3a9-1d7b-4449-a6ce-10ff6d2ba85f",
            "name": "Adult",
            "isChild": false
          },
          {
            "id": "2943ee0b-081f-4f77-a766-8e263dcdb442",
            "name": "Child",
            "isChild": true
          }
        ],
        "fullAddress": "1, Street Way, Road St",
        "status": "ACTIVE",
        "holderFirstName": "Test",
        "holderLastName": "Person",
        "markedForDeletion": false
      },
      ...
    ],
    "backwardEdge": "id:10715970-8aa8-4a54-9d74-c5dc6738364f,createdAt:1591369643939",
    "forwardEdge": "id:9abf5e8a-74dd-441d-a3a0-2c21fe608bb2,createdAt:1591365113606",
    "hasMore": true,
    "numberOfAllItems": 120,
    "numberOfPageItems": 1
  }
}
```

This endpoint retrieves all tickets that have either been updated or have expired between the supplied dates.

<aside class="notice">
Please note that a ticket which was <code>markedForDeletion</code> and has expired <em>will not</em> be returned by this endpoint.
</aside>

### HTTP Request

`https://garden-api.candideapp.com/ticket-updates`

### Query Parameters

| Parameter | Default | Description                                                                                       |
| --------- | ------- | ------------------------------------------------------------------------------------------------- |
| startDate |         | Filter out all records last updated before this date and time. ISO Format YYYY-MM-DDTHH:mm:ss UTC |
| endDate   | now     | Filter out all records last updated after this date and time                                      |
| after     |         | A cursor from the previous page. Use forwardEdge and backwardEdge to traverse pages               |
| limit     | 10      | The number of records per page                                                                    |
| sortOrder | ASC     | ASC or DESC                                                                                       |

## Get Ticket

```shell
curl "https://garden-api.candideapp.com/tickets/:id"
  -H "Authorization: plants-plants-plants"
```

> The above command returns JSON structured like this:

```json
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
  "visitorTypes": [
    {
      "id": "4356b3a9-1d7b-4449-a6ce-10ff6d2ba85f",
      "name": "Adult",
      "isChild": false
    },
    {
      "id": "2943ee0b-081f-4f77-a766-8e263dcdb442",
      "name": "Child",
      "isChild": true
    }
  ],
  "fullAddress": "1, Street Way, Road St",
  "status": "ACTIVE",
  "holderFirstName": "Test",
  "holderLastName": "Person",
  "markedForDeletion": false
}
```

This endpoint retrieves the spcified ticket by the provided id.

<aside class="notice">
Please note that requesting a ticket which has been deleted, whether due to an automated process or a GDPR request, will result in a <em>404</em> response.
</aside>

### HTTP Request

`https://garden-api.candideapp.com/tickets/:id`

### Query Parameters

| Parameter | Default | Description                             |
| --------- | ------- | --------------------------------------- |
| id        |         | The id of the ticket to fetch           |

# Check-ins

## Get All Check-ins

```shell
curl "https://garden-api.candideapp.com/checkins"
  -H "Authorization: plants-plants-plants"
```

> The above command returns JSON structured like this:

```json
{
  "checkins": {
    "results": [
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
    ],
    "backwardEdge": "id:61515eb4-10f7-4eed-b835-5fe385cf53cd,createdAt:1591092074828",
    "forwardEdge": "id:55c77fe7-4885-4a7a-a554-cdf9649f74d0,createdAt:1582733078354",
    "hasMore": false,
    "numberOfAllItems": 18,
    "numberOfPageItems": 2
  }
}
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
| after     |         | A cursor from the previous page. Use forwardEdge and backwardEdge to traverse pages  |
| limit     | 10      | The number of records per page                                                       |
| sortOrder | ASC     | ASC or DESC                                                                          |
