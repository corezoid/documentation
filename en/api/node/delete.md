# Removal of a node

Request
```json
{
  "ops": [
    {
      "type": "delete",
      "obj": "node",
      "obj_id": "537747241a8a387c62a59a02",
      "conv_id": "2427"
    }
  ]
}
```

Response if process is not found:
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "obj": "conv",
      "obj_id": "537747241a8a387c62a59a02",
      "proc": "ok"
    }
  ]
}
```
