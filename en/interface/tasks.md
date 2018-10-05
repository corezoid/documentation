# Tasks
Task - it is the tex file in JSON format. In such file you can find the information in `"parameter":"value"` format.

Example of task:

```json
{
        "create_time": "2015.11.10 18:13:29",
        "change_time": "2015.11.10 18:13:29",
        "node_prev_id": null,
        "status": "created",
        "user_id": 001,
        "data": {
                "message": {
                        "nick": "Vitaliy",
                        "message": "Hello, world!",
                }
        }
}
```

Every task contains proprietary information (`create_time`, `change_time`, `node_prev_id`, `status`, `user_id`) and data, that we can analyze and change during the process (`data`).

###Access to task's parameters

Access to contect of  `nick` parameter of this task has the following syntax: `{{message.nick}}`.


