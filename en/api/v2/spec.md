## Protocol description

Before you can start using Corezoid API you need to create `API key` and get **an authorization login** and **secret key**.

`Users & Groups -> Create -> API key -> enter name -> OK`

![](../img/create_api_key.gif)


**URL**

```
https://api.corezoid.com/api/2/json/{API_LOGIN}/{GMT_UNIXTIME}/{SIGNATURE}
```

* **{API_LOGIN}** - authorization login of your `API key`

* **{GMT_UNIXTIME}** - request time, a Unix timestamp (epoch time), by Greenwich (GMT+0), integer required parameter

* **{SIGNATURE}** - the signature

The signature is a concatenated string generated from the following parts:

`hex( sha1({GMT_UNIXTIME} + {API_SECRET} + {CONTENT} + {API_SECRET}) )`, where

* `hex()` - convert binary data to hexadecimal form
* `sha1()` - standart hash-function SHA-1, must return binary data
* `+` -  text string concatenation
* `{API_SECRET}` - a secret key of your `API key`
* `{CONTENT}` - request body

The whole request is http-body, it also described earlier in the signature formula as the `{CONTENT}`.

All text is expected to be encoded as **UTF-8**.
API request requires setting HTTP header:
`Content-type: application/json; charset=utf8`

**Request**

Request body contains a list of operations (**ops**):

```json
{
  "ops": [
    {
      "type": "create",
      "obj": "conv"
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n1234"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "obj": "conv",
      "obj_id": "1234",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n1234",
      "proc": "obj_id_not_found"
    }
  ]
}
```

| parameter | value | description |
| --- | --- | --- |
| request_proc | "ok" in the case of a successful request, otherwise - error | global status of whole package processing |
| ops | [] | list of operations |
| ops[n].proc | "ok" in the case of a successful request, otherwise - error | status for a separate operation |

