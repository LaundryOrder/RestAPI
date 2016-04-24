# Restful API 0.1

All request in json format

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
