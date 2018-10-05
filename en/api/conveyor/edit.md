# Refreshing desrcription of a process

Let us rename a process.

Request:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "conv",
      "obj_id": "1234",
      "title": "Process №1"
    }
  ]
}
```


In case of "modify" type operation changes concern only specified object parameters.

Any system elements may be edited in the same way.

Response in case of successful execution of operation:
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "obj": "conv",
      "obj_id": "1234",
      "proc": "ok"
    }
  ]
}
```
