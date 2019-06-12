# Protocol description

```http
https://api.corezoid.com/api/1/json/{API_LOGIN}/{GMT_UNIXTIME}/{SIGNATURE}
```

Where IDs in the curly brackets denote the following parameters:

*   `{API_LOGIN}` - [authorization login](../interface/users_groups.md) to API, you can receive it from service, required parameter.
*   `{GMT_UNIXTIME}` - request time, unix time format in seconds by Greenwich (GMT+0), integer required parameter.
*   `{SIGNATURE}` - request signature, required parameter, letter case is not important, calculated using the formula:
`hex( sha1({GMT_UNIXTIME} + {API_SECRET} + {CONTENT} + {API_SECRET}) )`, where
    *   `hex()` - function which convert binary data into hexadecimal format
    *   `sha1()` - standard hash-function SHA-1, must return binary data
    *   `+` -  text string concatenation
    *   `{API_SECRET}` - a secret key which is issued together with login `{API_LOGIN}`
    *   `{CONTENT}` - request body

The whole request is http-body, it also described earlier in the signature formula as the `{CONTENT}`. 

Text code is `utf-8`. It completely matches with standard and is sent together with next http-title:
*   For "json" protocol format:
`Content-type: application/json; charset=utf8`

Request contains operations list (array ops).

**Request**

```json
{
  "ops": [
    {
      "type": "create",
      "obj": "conv"/*…*/
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n1234"/*…*/
    }
  ]
}
```

*   type - operations type.
*   obj - object type which is being operated on.
*   obj_id - object ID which is being operated on.

**Response** is a list of operations results:
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
    }/*…*/
  ]
}
```
*   request_proc - global status of whole package processing, if "ok" - package is alright otherwise there's a mistake.
*   proc - operation processing status, if "ok" - successful execution otherwise there's a mistake (or there're special statuses of delayed operations).

Response in case of error for the whole package:
```json
{
  "request_proc": "format_error",
  "ops": [

  ]
}
```

In this case the operation list is empty because no operations were executed.
