# Removing a process

Let us try to remove a process with another identifier.

Request
```json
{
  "ops": [
    {
      "type": "delete",
      "obj": "conv",
      "obj_id": "9999"
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
      "obj": "conv",
      "obj_id": "9999",
      "proc": "obj_id_not_found"
    }
  ]
}
```

Any system elements can be removed in the same way.
