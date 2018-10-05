# Process logic

* [Adding logic](#add)
* [Managing logic](#managing)
* [Removing logic](#remove)


### Adding logic {#add}

Add logic to "Processing node" (node_id="n10221"):
*   when number of tasks in the node is over 1000, create escalation (simoultaneously) in "Escalation mode" (node_id="n10233").
*   time logic - 10 minutes (600 seconds). When task stays in the node more than specified time, limit is moved to "Final node, error" (node_id="n10234").

Request:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Database error",
      "obj_type": 3,
      "semaphors": [
        {
          "type": "count",
          "value": "1000",
          "esc_node_id": "n10233"
        },
        {
          "type": "time",
          "value": "600",
          "to_node_id": "n10234"
        }
      ]
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
      "obj": "node",
      "obj_id": "n10221",
      "proc": "ok"
    }
  ]
}
```
### RPC

```json
{
  "type": "api_rpc",
  "conv_id": 1,
  "extra": {
    "param1":"value"
  },
  "err_node_id": ""
}
```
### RPC reply

Two settings:
```json
{
  "type": "api_rpc_reply",
  "mode": "keys",
  "res_data": [
    "key1",
    "key2",
    "key3"
  ]
}
```

```json
{
  "type": "api_rpc_reply",
  "mode": "key_value",
  "res_data": {
    "key1":"value1",
    "key2":"value2",
    "key3":"value3",
  }
}
```

### Managing logic {#managing}

"Processing node" (node_id="n10221").

Let us add to "Processing node" (node_id="n10221"):
1.  Call of standard API (sent by 'res' parameter) on http://my_api.com/?f=json in json format.
2.  If 'res' parameter equals to "0" - go to "Final node, success" (node_id="n10222").
3.  Otherwise - go to "Final node, error" (node_id="n10234").

Request:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Database error",
      "obj_type": 3,
      "logics": [
        {
          "type": "api",
          "format": "json",
          "url": "http://my_api.com/?f=json"
        },
        {
          "type": "go_if_const",
          "param": "res",
          "fun": "eq",
          "const": "0",
          "to_node_id": "n10222"
        },
        {
          "type": "go",
          "to_node_id": "n10234"
        }
      ]
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
      "obj": "node",
      "obj_id": "n10221",
      "proc": "ok"
    }
  ]
}
```

### Removing logic {#remove}

Removal is made by deleting a node from JSON and sending request with the following parameters:
*   `type` = `modify`
*   `obj` = `node`

Request before removal:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Database error",
      "obj_type": 3,
      "logics": [
        {
          "type": "api",
          "format": "json",
          "url": "http://my_api.com/?f=json"
        },
        /// remove this logic block =======
        {
          "type": "go_if_const",
          "param": "res",
          "fun": "eq",
          "const": "0",
          "to_node_id": "n10222"
        },
        ///=================================
        {
          "type": "go",
          "to_node_id": "n10234"
        }
      ]
    }
  ]
}
```

Request after logic removal, ready for sending:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Database error",
      "obj_type": 3,
      "logics": [
        {
          "type": "api",
          "format": "json",
          "url": "http://my_api.com/?f=json"
        },
        {
          "type": "go",
          "to_node_id": "n10234"
        }
      ]
    }
  ]
}
```
