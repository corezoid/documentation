# Start/stop

To stop a process put it in a "blocked" status.

Request:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "conv",
      "obj_id": "1234",
      "status": "blocked"
    }
  ]
}
```

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

To launch a process put it in a "actived" status.

Request:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "conv",
      "obj_id": "1234",
      "status": "blocked"
    }
  ]
}
```

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
