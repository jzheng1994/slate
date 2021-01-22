---
title: MyRIACompliance API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the MyRIACompliance API. You can use our API to access certain information stored in our databases.

We have example code on the right that you can use in your own code.

# Authentication

> To authorize, use this code:

```shell
curl -X POST "https://api.myriacompliance.com/api/v1/token" 
  -H "accept: application/json; charset=UTF-8" 
  -H "Content-Type: application/json" 
  -d "{\"client_id\":\"client_id\",\"client_secret\":\"secret\",\"grant_type\":\"password\",\"username\":\"bob\",\"password\":\"password\"}"
```

```javascript
  const data = {
    "client_id": "client_id",
    "client_secret": "secret",
    "grant_type": "password",
    "username": "bob",
    "password": "password"
  };
  fetch("https://api.myriacompliance.com/api/v1/token", {
    method: 'POST'
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data);
  })
```

> The above command returns JSON structured like this:

```json
{
    "token_type": "Bearer",
    "expires_in": 86400,
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjNlZDQyYWVhMTE2YWQ4NDQ5MWE0ZDA1NWNjNjBjNWQzZDkxZDk3MjRkZTFiNDM0NWFhYWNkYmU3YWJmZTg3ZTdkNGIyODhmZjg4ODQxMmU5In0",
    "refresh_token": "def5020016bc35c7132e0a9fccb7f06b51825ad4a0c1c15b72d1d2d210747d34ba5252d92",
},
```

To generate an access token and refresh token, you must provide your client id and client secret along with your MyRIACompliance credentials.

Once generated, be sure to include the token in all API requests to the server in a header that looks like the following: 

`Authorization: Bearer {access_token}`

<aside class="notice">
You must replace <code>{access_token}</code> with your personal access token.
</aside>

<aside class="notice">
Remember to include your access token in all requests.
</aside>

# User / Firm Info 

## Get User

```shell
curl -X GET "https://api.myriacompliance.com/api/v1/user" 
  -H "accept: application/json" 
  -H "Authorization: Bearer {access_token}"
```

```javascript
 fetch("https://api.myriacompliance.com/api/v1/token", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  })
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "dt_created": "2015-01-01 00:00:00",
  "customer_login_type_id": 4,
  "username": "bob",
  "is_new_employee": 1,
  "dt_last_login": "2020-07-17 17:59:12",
  "login_count": 100,
  "phone": "(123) 456-7890",
  "email": "bob@gmail.com",
  "title": "",
  "crd": "1111111",
  "last_name": "Smith",
  "first_name": "Bob",
  "account_id": "FAKEACCOUNTID123",
  "is_access_person": 1,
  "external_id": null,
  "add_on_services": {
    "1": 1,
    "2": 1,
    "3": 1,
    "6": 1,
    "7": 1
  }
}
```

This endpoint retrieves the user's information.

### HTTP Request

`GET https://api.myriacompliance.com/api/v1/user`

## Update User Information

```shell
  curl -X PUT "https://api.myriacompliance.com/api/v1/user/{user_id}" 
  -H  "accept: application/json" 
  -H  "Authorization: Bearer {access_token}"
  -d '{"first_name":"Scotty","last_name":"Smith"}'
```

```javascript
   fetch("https://api.myriacompliance.com/api/v1/user/{user_id}", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "dt_created": "2015-01-01 00:00:00",
  "customer_login_type_id": 4,
  "username": "bob",
  "is_new_employee": 1,
  "dt_last_login": "2020-07-17 17:59:12",
  "login_count": 100,
  "phone": "(123) 456-7890",
  "email": "bob@gmail.com",
  "title": "",
  "crd": "1111111",
  "last_name": "Smith",
  "first_name": "Scotty",
  "account_id": "FAKEACCOUNTID123",
  "is_access_person": 1,
  "external_id": null,
  "add_on_services": {
    "1": 1,
    "2": 1,
    "3": 1,
    "6": 1,
    "7": 1
  }
}
```

This endpoint allows you to update certain fields for a user.

### HTTP Request

`PUT https://api.myriacompliance.com/api/v1/user/{user_id}`

### URL Parameters

| Parameter | Type | Description |
|-------------|-----|------------|
| **user_id** | int | User's ID  |

### Body Parameters

| Parameter             | Type   | Description               |
|-----------------------|--------|---------------------------|
| first_name (optional) | string | First name                |
| last_name (optional)  | string | Last name                 |
| email (optional)      | string | Email                     |
| title (optional)      | string | Title or Position of user |
| phone (optional)      | string | Phone number              |

<aside>A <b>supervisor</b> can edit any user's information as long as they are from the same firm.</aside>

## Get Firm Info

```shell
curl -X GET "https://api.myriacompliance.com/api/v1/firm" 
  -H  "accept: application/json" 
  -H  "Authorization: Bearer {access_token}"
```

```javascript
 fetch("https://api.myriacompliance.com/api/v1/firm", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
{
    "account_id": "0123456789ABCDEF",
    "iard": "1234567",
    "firm_name": "OBrien Asset Management LLC"
}
```

This endpoint retrieves a specific user's firm information.


### HTTP Request

`GET https://api.myriacompliance.com/api/v1/firm`

## Get Registration Statuses

```shell
  curl -X GET "https://api.myriacompliance.com/api/v1/firm_registrations_current"
    -H  "accept: application/json"
    -H  "Authorization: Bearer {access_token}"
```

```javascript
 fetch("https://api.myriacompliance.com/api/v1/firm_registrations_current", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
[
    {
        "iard": "01234567",
        "jurisdiction": "CA",
        "status": "Pending",
        "date_update": "2016-01-08"
    },
    {
        "iard": "01234567",
        "jurisdiction": "NY",
        "status": "Approved",
        "date_update": "2015-07-04"
    },
    {
        "iard": "01234567",
        "jurisdiction": "SEC",
        "status": "Approved",
        "date_update": "2016-11-11"
    },
]
```

This endpoint fetches all current registration statuses for a specific user's firm.

### HTTP Request

`GET https://api.myriacompliance.com/api/v1/firm_registrations_current`


## Get User's Current Registrations

```shell
  curl -X GET "https://api.myriacompliance.com/api/v1/individual_registrations_current" 
    -H  "accept: application/json" 
    -H  "Authorization: Bearer {access_token}"
```

```javascript
   fetch("https://api.myriacompliance.com/api/v1/individual_registrations_current", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
[
    {
        "iard": "01234567",
        "crd": "90807060",
        "first_name": "Matt",
        "last_name": "OBrien",
        "is_active": 1,
        "jurisdiction": "IN",
        "status": "DEFICIENT",
        "date_update": "2013-05-02"
    },
    {
        "iard": "01234567",
        "crd": "98765432",
        "first_name": "Matt",
        "last_name": "OBrien",
        "is_active": 1,
        "jurisdiction": "KY",
        "status": "PENDING",
        "date_update": "2013-05-02"
    },
    {
        "iard": "01234567",
        "crd": "98765432",
        "first_name": "Matt",
        "last_name": "OBrien",
        "is_active": 1,
        "jurisdiction": "OH",
        "status": "APPROVED",
        "date_update": "2013-05-16"
    }
]
```

Summary of the current individual registrations associated with the firm.

### HTTP Request

`GET https://api.myriacompliance.com/api/v1/individual_registrations_current`


### Query Parameters

| Parameter | Type | Description                                                                       |
|---------------|--------------|-----------------------------------------------------------------------|
| **is_active** | int (0 or 1) | Grab active or inactive registrations for this user. Defaults to all. |

## Update Jursidction Data

```shell
  curl -X POST "https://api.myriacompliance.com/api/v1/registration/jurisdictions" 
    -H  "accept: */*" 
    -H  "Authorization: Bearer {access_token}" 
    -H  "Content-Type: application/json" 
    -d "{\"jurisdictions\":[{\"state\":\"NY\",\"clients\":8},{\"state\":\"CA\",\"clients\":2},{\"state\":\"MD\",\"clients\":12}]}"
```

```javascript
  const data = {
    "jurisdictions": [
      {"state":"NY","clients":8},
      {"state":"CA","clients":2},
      {"state":"MD","clients":12}
     ]
  };
   fetch("https://api.myriacompliance.com/api/v1/registration/jurisdictions", {
    method: 'POST'
    headers: {
      'Authorization': `Bearer ${access_token}`
    },
    body: JSON.stringify(data)
  });
```

> The above command returns JSON structured like this:

```json
"OK"
```

This endpoint allows you to update your jurisdiction data.

### HTTP Request

`POST https://api.myriacompliance.com/api/v1/registration/jurisdictions`

### Body Parameters

| Parameter | Type | Description                                |
|-------------------|--------------|----------------------------|
| **jurisdictions** | array        | Array of jurisdiction data |

## Update Firm AUM 

```shell
  curl -X POST "https://api.myriacompliance.com/api/v1/registration/aum" 
    -H  "accept: */*" 
    -H  "Authorization: Bearer {access_token}" 
    -H  "Content-Type: application/json" 
    -d "{\"aum\":{\"disc\":65000,\"non_disc\":233500}}"
```

```javascript
  const data = {
    "aum": {"disc":65000,"non_disc":233500}
  }
   fetch("https://api.myriacompliance.com/api/v1/registration/aum", {
   method: 'POST'
    headers: {
      'Authorization': `Bearer ${access_token}`
    },
    body: JSON.stringify(data)
  });
```

> The above command returns JSON structured like this:

```json
"OK"
```

This endpoint allows you to update your firm's AUM.

### HTTP Request

`POST https://api.myriacompliance.com/api/v1/registration/aum`

### Body Parameters

| Parameter | Type | Description                                         | 
|-----|--------|---------------------------------------------------------|
| aum | object | Object containing firm's disclosed and nondisclosed AUM |

## Update Firm's total accounts

```shell
  curl -X POST "https://api.myriacompliance.com/api/v1/registration/accounts" 
    -H  "accept: */*" 
    -H  "Authorization: Bearer {access_token}" 
    -H  "Content-Type: application/json" 
    -d "{\"accounts\":{\"non_disc\":25,\"disc\":null}}"
```

```javascript
  const data = {
    "accounts":{"non_disc":25, "disc":null}
  };
   fetch("https://api.myriacompliance.com/api/v1/registration/accounts", {
   method: 'POST'
    headers: {
      'Authorization': `Bearer ${access_token}`
    },
    body: JSON.stringify(data)
  });
```

> The above command returns JSON structured like this:

```json
"OK"
```

This endpoint allows you to update your firm's total accounts.

### HTTP Request

`POST https://api.myriacompliance.com/api/v1/registration/accounts`

### Body Parameters

| Parameter | Type | Description                                    | 
|----------|--------|-----------------------------------------------|
| accounts | object | Object containing firm's accounts information |

# Calendar 

## Calendar Items

```shell
  curl -X GET "https://api.myriacompliance.com/api/v1/calendarevents" 
    -H  "accept: application/json"
    -H  "Authorization: Bearer {access_token}"
```

```javascript
   fetch("https://api.myriacompliance.com/api/v1/calendarevents", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": 344542,
        "is_custom": 0,
        "date_due": "2019-07-27",
        "client_date_due": "2019-07-24",
        "title": "Policies and Procedures Manual Review",
        "assigned_to_user_id": null,
        "date_assigned_to_user": null,
        "is_completed": 1,
        "dt_completed": "2019-07-24 00:00:00",
        "category": 2,
        "type": 1,
        "description": "This review ensures that your P&P manual is current with your own internal policies and the regulations governing your activities."
    },
    {
        "id": 345291,
        "is_custom": 0,
        "date_due": "2017-12-31",
        "client_date_due": "2017-12-31",
        "title": "Passwords Update",
        "assigned_to_user_id": null,
        "date_assigned_to_user": null,
        "is_completed": 0,
        "dt_completed": null,
        "category": 2,
        "type": 1,
        "description": "Updating firm and individual passwords mitigates a major risk associated with a cybersecurity breach."
    },
    {
        "id": 345521,
        "is_custom": 0,
        "date_due": "2018-05-08",
        "client_date_due": "2018-05-08",
        "title": "Advertising Review",
        "assigned_to_user_id": null,
        "date_assigned_to_user": null,
        "is_completed": 0,
        "dt_completed": null,
        "category": 2,
        "type": 1,
        "description": "This review confirms that investment advice is being provided in accordance with each sampled client’s investment objectives."
    },
]
```

This endpoint fetches calendar item(s) for a specific user.

### HTTP Request

`GET https://api.myriacompliance.com/api/v1/calendarevents`

### Query Parameters

| Parameter  | Type                                        | Description                                                          |                            
|-----------------------|-----------------------------------------------|---------------------------------------------------------|
| start_date (optional) | ISO8601 Formatted DateString (Ex: 2016-01-01) | Fetch calendar items whose due date is after this date  |
| end_date (optional)   | ISO8601 Formatted DateString (Ex: 2020-01-01) | Fetch calendar items whose due date is before this date |

## Get Single Calendar Item By ID
 
```shell
  curl -X GET "https://api.myriacompliance.com/api/v1/calendarevents/{item_id}" 
    -H  "accept: application/json" 
    -H  "Authorization: Bearer {access_token}"
```

```javascript
   fetch("https://api.myriacompliance.com/api/v1/calendarevents/{item_id}", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
    {
        "id": 345521,
        "is_custom": 0,
        "date_due": "2018-05-08",
        "client_date_due": "2018-05-08",
        "title": "Advertising Review",
        "assigned_to_user_id": null,
        "date_assigned_to_user": null,
        "is_completed": 0,
        "dt_completed": null,
        "category": 2,
        "type": 1,
        "description": "This review confirms that investment advice is being provided in accordance with each sampled client’s investment objectives."
    },
```

This endpoint fetches a specific calendar item by its ID.

### HTTP Request

`GET https://api.myriacompliance.com/api/v1/calendarevents/{item_id}`

### URL Parameters

| Parameter | Type | Description          |                                                                          
|---------|-----|-------------------------|
| item_id | int | ID of the calendar item |

<aside class="warning">An invalid calendar item ID will return an empty json response</aside>

## Mark Calendar Item Complete

```shell
  curl -X PUT "/api/v1/calendarevents/{item_id}" 
    -H  "accept: application/json" 
    -H  "Authorization: Bearer {access_token}"
```

```javascript
  const data = {'date_completed': '2020-05-20'};
   fetch("/api/v1/calendarevents/{item_id}", {
    method: 'PUT',
    headers: {
      'Authorization': `Bearer ${access_token}`
    },
    body: JSON.stringify(data)
  });
```

> The above command returns JSON structured like this:

```json
{
    "Updated": "Marked as completed successfully"
}
```

This endpoint allows you to mark a calendar item as complete.

### HTTP Request

`PUT /api/v1/calendarevents/{item_id}`

### URL Parameters

| Parameter | Type | Description          |                                                                          
|---------|-----|-------------------------|
| item_id | int | ID of the calendar item |

### Query Parameters

| Parameter | Type | Description                                               |                                                                          
|----------------|-------------------------------|-----------------------------|
| date_completed | ISO8601 Date Formatted String | Date the item was completed |

# To-Dos

## User To-dos

```shell
  curl -X GET "https://api.myriacompliance.com/api/v1/todos" 
    -H  "accept: application/json" 
    -H  "Authorization: Bearer {access_token}"
```

```javascript
   fetch("/api/v1/todos", {
    headers: {
      'Authorization': `Bearer ${access_token}`
    }
  });
```

> The above command returns JSON structured like this:

```json
{
    "success": true,
    "error": null,
    "payload": [
        {
            "label": "Review Q3 2019 Gifts and Entertainment to/from Clients",
            "status": null,
            "description": "Please review your Gifts and Entertainment to/from Clients activity requests for the past period specified and confirm their accuracy and completeness."
        },
        {
            "label": "Review Q3 2019 Social Media Usage",
            "status": null,
            "description": "Please review your Social Media Usage activity requests for the past period specified and confirm their accuracy and completeness."
        },
        {
            "label": "Review Q3 2019 Advertising and Marketing",
            "status": null,
            "description": "Please review your Advertising and Marketing activity requests for the past period specified and confirm their accuracy and completeness."
        },
        {
            "label": "Review August 2019 Outside Business Activities",
            "status": null,
            "description": "Please review your Outside Business Activities activity requests for the past period specified and confirm their accuracy and completeness."
        },
    ]
}
```

This endpoint allows you to fetch all the todos for a specific user as well as any calendar items assigned to the user.

### HTTP Request

`GET /api/v1/todos` 


<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->