# Restful API 0.1

All request in json format

All request url is prefixed with "protocol://hostname:port/api

## Auth

### Login

method

`POST /login`

data

```json
{
  "username":"...",
  "password":"..."
}
```

return

```json
{
  "token":"..."
}
```

### Register

method

`POST /register`

data

```json
{
  "username":"...",
  "password":"..."
}
```

return

```json
{
  "token":"..."
}
```

All request below need a token to process, or a 403 with message will be returned.

## Inquery available time

method

`GET /available`

data

`none`

return

```json
{
  "available":[
    {
      "start": 140000000,
      "end": 1400000001
    },
    {
      "start" : 140000002,
      "end": 1400000006
    }
  ]
}
```
## Make an appointment

method

`POST /order`

data

```json
{
  "start": 140000002,
  "end": 1400000003,
  "door": {
    "start": 1400000001,
    "end": 1400000006,
    "phone": 13800138000,
    "addr": "foo, St. bar"
  }
}
```

return

```json
{
  "success": 1,
  "order_id": 233
}
```

## Cancel an appointment

method

`DELETE /order/233`

data

`none`

return

```json
{
  "success": 1
}
```

## Modify a appointment

method

`PATCH /order/233`

data

```json
{
  "start": 140000002,
  "end": 1400000003,
  "door": {
    "start": 1400000001,
    "end": 1400000006,
    "phone": 13800138000,
    "addr": "foo, St. bar"
  }
}
```

return

```json
{
  "success": 1
}
```

## Get info of an appointment

method

`GET /order/233`

data

`none`

return

```json
{
  "start": 140000002,
  "end": 1400000003,
  "door": {
    "start": 1400000001,
    "end": 1400000006,
    "phone": 13800138000,
    "addr": "foo, St. bar"
}
```

## Get appointment list

method

`GET /orders`

data

`none`

return
```json
{ 
  "appointments":[
  {
    "status": "completed",
    "start": 140000002,
    "end": 1400000003,
    "door": {
      "start": 1400000001,
      "end": 1400000006,
      "phone": 13800138000,
      "addr": "foo, St. bar"
    }
  }]
}
```
