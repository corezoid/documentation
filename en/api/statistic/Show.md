# Show - Statistics on a chosen node for a certain period

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

