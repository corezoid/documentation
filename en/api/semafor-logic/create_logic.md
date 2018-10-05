# Managing logic

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


