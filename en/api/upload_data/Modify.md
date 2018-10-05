# Modify - Change of request in process by means of callback

Request with reference `130605ref1` sent for processing to http://my.api.com/getData via [api](external_api.md) method. Processing of request on api.my.com resource is made asynchronously, therefore after processing process receives callback with results.
**Example of callback to a process:**

Example of URL to which requests will be sent to: https://api.corezoid.com/api/1/json/13000/{GMT_UNIXTIME}/{SIGNATURE}


```json
{
    "ops":[
        {
            "type":"modify",
            "obj":"task",
            "ref":"130605ref1",
            "conv_id":"1234",
            "data":{
                "checkedClient":"true"
            }
        }
    ]
}
```

**Response of a process after callback successfully accepted:**
```json
{
    "request_proc":"ok",
    "ops":[
        {
            "ref":"130605ref4",
            "proc":"ok"
        }
    ]
}
```

`"checkedClient":"true"` - this parameter and its value will be added to the request with `130605ref1` reference. After that request leaves standby mode in `api_callback` and proceeds to perform the following logics.



