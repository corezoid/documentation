# Getting statistcs

* [Current value of the counter nodes by ID diagrams](#list)
* [Getting statistics on the ID diagrams and the node for the period](#show)

### Current value of the counter nodes by ID diagrams {#list}

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
               "title":"Request to database",
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
               "title":"Exit",
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
               "title":"Have you found a client in database by the phone?",
               "description":"undefined",
               "logics":[

               ],
               "semaphores":[

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
               "semaphors":[

               ],
               "count":0,
               "obj_type":1
            }
         ]
      }
   ]
}
```

### Getting statistics on the ID diagrams and the node for the period {#show}

Input parameters:
*   type - show type
*   obj - stat
*   conv_id - process ID
*   start - period "from" in UNIX format
*   end - period "to" in UNIX format
*   interval - for what intervals statistics will be provided
    *   day - by days
    *   hour - by hours
    *   minute - by minutes
*   group -
*   node_id - node ID

**Request:**
```json
{
   "ops":[
      {
         "type":"show",
         "obj":"stat",
         "conv_id":270,
         "start":1399410000,
         "end":1399496340,
         "interval":"hour",
         "group":"time",
         "node_id":"52a0706f10e87b488c597b01"
      }
   ]
}
```

**Response:**
```json
{
   "request_proc":"ok",
   "ops":[
      {
         "id":"",
         "proc":"ok",
         "obj":"stat",
         "group":"time",
         "conv_id":270,
         "data":[
            {
               "date":"2014-05-07 00:00:00",
               "in":48525,
               "out":48525
            },
            {
               "date":"2014-05-07 01:00:00",
               "in":122499,
               "out":122499
            },
            {
               "date":"2014-05-07 02:00:00",
               "in":383300,
               "out":383300
            },
            {
               "date":"2014-05-07 03:00:00",
               "in":36449,
               "out":36449
            },
            {
               "date":"2014-05-07 04:00:00",
               "in":7145,
               "out":7145
            },
            {
               "date":"2014-05-07 05:00:00",
               "in":20389,
               "out":20389
            },
            {
               "date":"2014-05-07 06:00:00",
               "in":33144,
               "out":33144
            },
            {
               "date":"2014-05-07 07:00:00",
               "in":110780,
               "out":110780
            },
            {
               "date":"2014-05-07 08:00:00",
               "in":328013,
               "out":328013
            },
            {
               "date":"2014-05-07 09:00:00",
               "in":535760,
               "out":535760
            },
            {
               "date":"2014-05-07 10:00:00",
               "in":556079,
               "out":556079
            }
         ]
      }
   ]
}
```

In every `"obj":"node"` element there is a `count` parameter - current number of requests in the node.
