# Nodes in the processes

* [Adding a node](#add)
* [Getting list of nodes](#get)
* [Removing a node](#remove)

### Adding a node {#add}

Let us create several nodes in one process.

Request:
```json
{
  "ops": [
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Processing node",
      "description": "This is starting node …",
      "obj_type": "1"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Final node, success",
      "obj_type": "2"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Escalation node",
      "obj_type": "3"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Final node, error",
      "obj_type": "2"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Escalation node, final",
      "obj_type": "2"
    }
  ]
}
```

`obj_type` defines type of a node:
*   0 - custom
*   1 - start (one process can have only one start nod)
*   2 - final
*   3 - escalation

Response in case of successful execution of operation:
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "obj": "node",
      "obj_id": "n10221",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n10222",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n10233",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n10234",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n10235",
      "proc": "ok"
    }
  ]
}
```

### Getting list of nodes {#get}

**Request:**
```json
{
    "ops":[
        {
            "type":"list",
            "obj":"conv",
            "obj_id":"260"
        }
    ]
}
```

**Response in case of successful execution of operation:**
```json
{
   "request_proc":"ok",
   "ops":[
      {
         "id":"",
         "obj":"conv",
         "obj_id":260,
         "privs":[
            "supers"
         ],
         "proc":"ok",
         "list":[
            {
               "obj":"node",
               "obj_id":"52988d1410e87b7d4410186d",
               "title":"Request to clients database",
               "description":"undefined",
               "logics":[
                  {
                     "type":"api",
                     "format":"json",
                     "url":"http://my.api.com/",
                     "extra":{
                        "idClient":"{{idClient}}"
                     },
                     "max_theads":"",
                     "err_node_id":"52fa3b7a10e87b098d49aba2"
                  },
                  {
                     "type":"go",
                     "format":"json",
                     "to_node_id":"52f4e08810e87b098dba2f1b",
                     "node_title":"Have you found a client?"
                  }
               ],
               "semaphores":[

               ],
               "count":0,
               "obj_type":0
            },
            {
               "obj":"node",
               "obj_id":"52988d1b10e87b7d44101a3e",
               "title":"Logout",
               "description":"",
               "logics":[

               ],
               "semaphores":[

               ],
               "count":4,
               "obj_type":2
            },
            {
               "obj":"node",
               "obj_id":"52f4e08810e87b098dba2f1b",
               "title":"Have you found a client in database by phone?",
               "description":"undefined",
               "logics":[

               ],
               "semaphors":[

               ],
               "count":0,
               "obj_type":0
            },
            {
               "obj":"node",
               "obj_id":"52fa3b7a10e87b098d49aba2",
               "title":"Database error",
               "description":"",
               "logics":[

               ],
               "semaphores":[

               ],
               "count":2,
               "obj_type":2
            },
            {
               "obj":"node",
               "obj_id":"52fa3bd310e87b098d49e425",
               "title":"Start",
               "description":"undefined",
               "logics":[
                  {
                     "type":"go",
                     "format":"json",
                     "to_node_id":"52988d1410e87b7d4410186d"
                  }
               ],
               "semaphores":[

               ],
               "count":0,
               "obj_type":1
            }
         ]
      }
   ]
}
```

### Removing of a node {#remove}

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
