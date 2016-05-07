# Restful API 0.1

All request in json format

All request url is prefixed with "protocol://hostname:port/api

`"success":1` means success, if error occurred, `"success":0` shall be return with an error message `"msg":"failure reason"`

# Auth

All request except Login or Register need a token to process, or an error message shall be returned.

Token shall be sent in http header, Authorization: Token XXX

## Login or Register

method

`POST /token`

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

## Logout

method

`GET /revoke`

data

`none`

return

```json
{
  "success":1
}
```

## Inquiry available time

pair timestamp with `"start"` and `"end"` means a span of time

method

`GET /avail`

data

`none`

return

```json
{
  "time":140000001
}
```

# Appointment

an appointment may contains all/part of following property/object

```json
{
  "order_id": 233
  "start":140000001,
  "end":140000002,
  "machine":1,
  "order_time": 140000000,
  "order_token": "asdf",
  "status": 1,
  "door":{}
}
```

json above is an *appointment object* indicate a certain appointment

order_id: the id of the order

start: appointment start time, in unix timestamp format(same with following time)

end: appointment end time

machine: which machine shall process this order

order_time: time the appointment made

order_token: token to prove the order owner

status: order status, 1 for canceled, 2 for completed, 3 for engaging

door: door service, contains following property

```json
{
  "start": 14000001,
  "end": 14000002,
  "order_time": 14000000,
  "phone": "13800013800",
  "address": "Foo, St. Bar"
}
```

json above is a *door object* indicate a certain door service

start: door service start time

end: door service end time

order_time: time the door service order made

phone: phone number of the customer

address: address of the customer

## Make an appointment

method

`POST /order`

data

an *appointment object* that only contain "`door`", and *door object* can only contain `"phone", "address"`

return

*appointment object*

## Cancel an appointment

method

`DELETE /order/233`

where 233 is the order id

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

`PUT /order/233`

where 233 is the order id

data

any property/object(s) of an *appointment object* without `"order_token", "order_time", "status"`

return

```json
{
  "success": 1,
  "order_id": 233
}
```

## Get info of an appointment

method

`GET /order/233`

data

`none`

return

if an *appointment object*

## Get appointment list

method

`GET /orders`

data

`none`

return

```json
{ 
  "orders":[]
}
```
`"orders"` is a list of *appointment object*
