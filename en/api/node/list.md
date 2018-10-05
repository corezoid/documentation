# Receiving a list of nodes

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
