# Operations with tasks

*   [Create task](#create-task)
*   [Modify task](#modify-task)
*   [Show task](#show-task)
*   [Delete task](#delete-task)

## Create task

**Request**

```json
{
  "ops": [
    {
      "type": "create",
      "conv_id": "{{process_id}}",
      "obj": "task",
      "data": {
        "test_id": "xxx"
      },
      "ref": "{{ref}}",
      "id": "{{id}}"
    }
  ]
}
```

| parameter | accept type | description | required | possible value |
| --- | --- | --- | --- | --- |
| ops| JSON Object | Parameter in which JSON objects with operations are transmitted  | + | * The number of operations is restricted by user limits. |
| type | string | Type of action | + | create |
| conv_id | number / number as string | Identifier of the process in which the application is created | + | Identifier of an existing process |
| obj | string | Type of object | + | task |
| data | JSON Object | Object with key-value pairs describing the necessary parameters | + | ** Number of parameters is not limited |
| ref | string / number / null | *** External identifier of the task | - | Any characters can be used, the length is limited to the range from 1 to 255 characters and the "ref" parameter  must be unique within all active objects of this type |
| id | string / number | **** Parameter to identify the operation in the ops array | - | Any characters can be used, the length is limited by the size of the HTTP request |

*See license agreement

**Task is limited only by the size specified in the configuration file

***Required to modify task

****The parameter is used in any queries to identify the operation in the ops array

### Sample request with the creation of a task

Creating a request with one parameter (key "test_id", value 123) in the process with identifier - 12345 and reference - 1559655803

**Request**

```json
{
  "ops": [
    {
      "type": "create",
      "conv_id": 12345,
      "obj": "task",
      "data": {
        "test_id": "123"
      },
      "ref": "1559655803"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655803",
      "obj_id": "5cf67011094bab1b9a00a31d"
    }
  ]
}
```

| parameter | description |
| --- | --- |
| request_proc | The overall processing status of all transactions from the request |
| ops | Parameter in which JSON objects with operations are transmitted |
| id | Parameter to identify the operation in the ops array |
| proc | The processing status of a specific operation |
| ref | External identifier of the task |
| obj_id | Identifier of the created object (task) |

### Sample request with the creation of several tasks

**Request**

```json
{
  "ops": [
    {
      "type": "create",
      "conv_id": 12345,
      "obj": "task",
      "data": {
        "test_id": "123"
      },
      "ref": "1559655803",
      "id": "1a"
    },
    {
      "type": "create",
      "conv_id": 12346,
      "obj": "task",
      "data": {
        "client_id": "00001"
      },
      "ref": "1559655804",
      "id": "2b"
    },
    {
      "type": "create",
      "conv_id": 12347,
      "obj": "task",
      "data": {
        "status": "IN"
      },
      "ref": "1559655805",
      "id": "3c"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "1a",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655803",
      "obj_id": "5cf67011094bab1b9a00a31d"
    },
    {
      "id": "3c",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655805",
      "obj_id": "5cf66ae256167c6c7f00a26d"
    },
    {
      "id": "2b",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655804",
      "obj_id": "5cf66b9856167c6c7f00a278"
    }
  ]
}
```


## Modify task

**Request**

```json
{
  "ops": [
    {
      "type": "modify",
      "conv_id": "{{process_id}}",
      "obj": "task",
      "data": {
        "test_id": "xxx"
      },
      "ref": "{{ref}}",
      "id": "{{id}}"
    }
  ]
}
```

| parameter | accept type | description | required | possible value |
| --- | --- | --- | --- | --- |
| ops| JSON Object | Parameter in which JSON objects with operations are transmitted  | + | * The number of operations is restricted by user limits. |
| type | string | Type of action | + | modify |
| conv_id | number / number as string | Identifier of the process in which the application is created | + | Identifier of an existing process |
| obj | string | Type of object | + | task |
| data | JSON Object | Object with key-value pairs describing the necessary parameters | + | ** Number of parameters is not limited |
| ref | string / number / null | External identifier of the task | + | Any characters can be used, the length is limited to the range from 1 to 255 characters and the "ref" parameter  must be unique within all active objects of this type |
| id | string / number | *** Parameter to identify the operation in the ops array | - | Any characters can be used, the length is limited by the size of the HTTP request |

*See license agreement

**Task is limited only by the size specified in the configuration file

***The parameter is used in any queries to identify the operation in the ops array

### Sample request with one modified task

Modification of the task with one parameter (the "user_id" key and the value 777 can be modified) in the process with the identifier - 12345 and the reference - 1559655803

**Request**

```json
{
  "ops": [
    {
      "type": "modify",
      "conv_id": 12345,
      "obj": "task",
      "data": {
        "user_id": "777"
      },
      "ref": "1559655803"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655803",
      "obj_id": "5cf67011094bab1b9a00a31d"
    }
  ]
}
```

| parameter | description |
| --- | --- |
| request_proc | The overall processing status of all transactions from the request |
| ops | Parameter in which JSON objects with operations are transmitted |
| id | Parameter to identify the operation in the Ops array |
| proc | The processing status of a specific operation |
| ref | External identifier of the task |
| obj_id | Identifier of the created object (task) |

### Sample request with the modification of several tasks

**Request**

```json
{
  "ops": [
    {
      "type": "modify",
      "conv_id": 12345,
      "obj": "task",
      "data": {
        "test_id": "123"
      },
      "obj_id": "5cf67011094bab1b9a00a31d",
      "id": "1a"
    },
    {
      "type": "modify",
      "conv_id": 12346,
      "obj": "task",
      "data": {
        "client_id": "00001"
      },
      "ref": "1559655804",
      "id": "2b"
    },
    {
      "type": "modify",
      "conv_id": 12347,
      "obj": "task",
      "data": {
        "status": "IN"
      },
      "ref": "1559655805",
      "id": "3c"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "1a",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655803",
      "obj_id": "5cf67011094bab1b9a00a31d"
    },
    {
      "id": "3c",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655805",
      "obj_id": "5cf66ae256167c6c7f00a26d"
    },
    {
      "id": "2b",
      "proc": "ok",
      "obj": "task",
      "ref": "1559655804",
      "obj_id": "5cf66b9856167c6c7f00a278"
    }
  ]
}
```

> Task modification may be carried out by "ref" or "obj_id".

## Show task

**Request**

```json
{
  "ops": [
    {
      "type": "show",
      "conv_id": "{{process_id}}",
      "obj": "task",
      "ref": "{{ref}}",
      "id": "{{id}}"
    },
    {
      "type": "show",
      "conv_id": "{{process_id}}",
      "obj": "task",
      "obj_id": "{{obj_id}}",
      "id": "{{id}}"
    }
  ]
}
```

| parameter | accept type | description | required | possible value |
| --- | --- | --- | --- | --- |
| ops| JSON Object | Parameter in which JSON objects with operations are transmitted  | + | * The number of operations is restricted by user limits. |
| type | string | Type of action | + | create |
| conv_id | number / number as string | Identifier of the process in which the application is created | + | Identifier of an existing process |
| obj | string | Type of object | + | task |
| obj_id | string | Identifier of the object (task) in the system | + | Identifier of an existing object |
| ref | string / number / null | External identifier of the task | - | Any characters can be used, the length is limited to the range from 1 to 255 characters and the "ref" parameter  must be unique within all active objects of this type |
| id | string / number | ** Parameter to identify the operation in the ops array | - | Any characters can be used, the length is limited by the size of the HTTP request |

*See license agreement

**The parameter is used in any queries to identify the operation in the ops array

### Sample request to show one task

Viewing task in the process with the identifier - 12345, the reference - 1559655803 and the object identifier - 5cf7738c094bab29da000d5a \

> Viewing of the task can be performed separately according to its reference or identifier

**Request**

```json
{
  "ops": [
    {
      "type": "show",
      "conv_id": 12345,
      "obj": "task",
      "ref": "1559655803",
      "id": "1"
    },
    {
      "type": "show",
      "conv_id": 12345,
      "obj": "task",
      "obj_id": "5cf7738c094bab29da000d5a",
      "id": "2"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "1",
      "proc": "ok",
      "obj": "task",
      "obj_id": "5cf7738c094bab29da000d5a",
      "ref": "1559655803",
      "status": "active",
      "user_id": 5555,
      "create_time": 1559722938,
      "change_time": 1559722943,
      "node_id": "5cf66f44094bab1b9a00a316",
      "node_prev_id": "5cf66f3d094bab1b9a00a314",
      "data": {
        "test_id": "***"
      }
    },
    {
      "id": "2",
      "proc": "ok",
      "obj": "task",
      "obj_id": "5cf7738c094bab29da000d5a",
      "ref": "1559655803",
      "status": "active",
      "user_id": 5555,
      "create_time": 1559722938,
      "change_time": 1559722943,
      "node_id": "5cf66f44094bab1b9a00a316",
      "node_prev_id": "5cf66f3d094bab1b9a00a314",
      "data": {
        "test_id": "***"
      }
    }
  ]
}
```

| parameter | description |
| --- | --- |
| request_proc | The overall processing status of all transactions from the request |
| ops | Parameter in which JSON objects with operations are transmitted |
| id | Parameter to identify the operation in the Ops array |
| proc | The processing status of a specific operation |
| obj | Type of object - task |
| obj_id | Identifier of the created object (task) |
| ref | External identifier of the task |
| status | Current task status |
| user_id | Identifier of user who created task |
| create_time | Time of task creation in Unix Time|
| change_time | Time of task modification in Unix Time |
| node_id | Identifier of the node where the task is located |
| node_prev_id | Identifier of the node from which the task was delivered to the current node |
| data | Object with key-value pairs describing the necessary parameters |

[Parameter Types and Parameter Management](https://doc.corezoid.com/en/interface/tasks/)

## Delete task

**Request**

```json
{
  "ops": [
    {
      "type": "delete",
      "conv_id": "{{process_id}}",
      "obj": "task",
      "obj_id": "{{obj_id}}",
      "node_id": "{{node_id}",
      "id": "{{id}}"
    }
  ]
}
```

| parameter | accept type | description | required | possible value |
| --- | --- | --- | --- | --- |
| ops| JSON Object | Parameter in which JSON objects with operations are transmitted  | + | * The number of operations is restricted by user limits. |
| type | string | Type of action | + | create |
| conv_id | number / number as string | Identifier of the process in which the application is created | + | Identifier of an existing process |
| obj | string | Type of object | + | task |
| obj_id | string | Identifier of the object (task) in the system | + | Identifier of an existing object |
| node_id | string | Identifier of the node where the task is located  | + | Identifier of an existing node |
| id | string / number | ** Parameter to identify the operation in the ops array | - | Any characters can be used, the length is limited by the size of the HTTP request |

*See license agreement

**The parameter is used in any queries to identify the operation in the ops array

### Sample request to delete one task

Deleting task with an object identifier - 5cf7c0bb094bab1d7a006c1e from a node with an identifier - 5cf66f44094bab1b9a00a316 in the process with an identifier - 12345

**Request**

```json
{
  "ops": [
    {
      "type": "delete",
      "obj": "task",
      "conv_id": 12345,
      "node_id": "5cf66f44094bab1b9a00a316",
      "obj_id": "5cf7c0bb094bab1d7a006c1e"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "proc": "ok",
      "obj": "task",
      "obj_id": "5cf7c0bb094bab1d7a006c1e"
    }
  ]
}
```

*Actual deletion of the task can be performed from 100 to 500 ms


| parameter | description |
| --- | --- |
| request_proc | The overall processing status of all transactions from the request |
| ops | Parameter in which JSON objects with operations are transmitted |
| id | Parameter to identify the operation in the ops array |
| proc | The processing status of a specific operation |
| obj | Type of object - task |
| obj_id | Identifier of the created object (task) |

### Sample request to delete a few tasks

**Request**

```json
{
  "ops": [
    {
      "type": "delete",
      "obj": "task",
      "conv_id": 12345,
      "node_id": "5cf66f44094bab1b9a00a316",
      "obj_id": "5cf7c0bb094bab1d7a006c1e",
      "id": "1a"
    },
    {
      "type": "delete",
      "obj": "task",
      "conv_id": 12345,
      "node_id": "6cf66f44094bab1b9a00a316",
      "obj_id": "6cf7c0bb094bab1d7a006c1e",
      "id": "2b"
    },
    {
      "type": "delete",
      "obj": "task",
      "conv_id": 12345,
      "node_id": "7cf66f44094bab1b9a00a316",
      "obj_id": "7cf7c0bb094bab1d7a006c1e",
      "id": "3c"
    }
  ]
}
```

**Response**

```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "1a",
      "proc": "ok",
      "obj": "task",
      "obj_id": "5cf7c0bb094bab1d7a006c1e"
    },
    {
      "id": "3c",
      "proc": "ok",
      "obj": "task",
      "obj_id": "7cf7c0bb094bab1d7a006c1e"
    },
    {
      "id": "2b",
      "proc": "ok",
      "obj": "task",
      "obj_id": "6cf7c0bb094bab1d7a006c1e"
    }
  ]
}
```
