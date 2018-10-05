# Removing logic

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
