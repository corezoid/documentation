# State diagrams/processes

Using API Corezoid you can create, modify, delete process (if your API key has access rights).

* [Process creation](#process-creation)
* [Process status change](#process-status-change)
* [Process renaming](#process-renaming)
* [Process removing](#process-removing)

### Process creation

Let us create a process. To launch a process put it in a "actived" status.

**Request**

```json
{
  "ops": [
    {
      "type": "create",
      "obj": "conv",
      "title": "My process",
      "description": "Here will be a detailed description of process",
      "status": "actived"
    }
  ]
}
```

If `status` is not specified, the value be `actived` by default.

Possible values of `status` parameter:
*   actived
*   paused
*   blocked

Response in case of successful operation execution:

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

### Process status change

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

**Request**

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "conv",
      "obj_id": "1234",
      "status": "actived"
    }
  ]
}
```

**Response** in case of successful execution of operation:

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

### Process renaming

Changes process title

**Request**

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

**Response** in case of successful execution of operation:

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

### Process removing

Remove process (move to Trash).

**Request**

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

**Response** if process is not found:

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
