# Получение статистики

*   [Текущие значение счетчиков узлов по ID диаграммы](#текущие-значение-счетчиков-узлов-по-id-диаграммы)
*   [Получение статистики по идентификатору диаграммы и узла за период](#получение-статистики-по-id-диаграммы-и-узла-за-период)


##Текущие значение счетчиков узлов по ID диаграммы

**Запрос:**
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

**Ответ при удачном выполнении операции:**
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
               "title":"Запрос в ЕКБ",
               "description":"undefined",
               "logics":[
                  {
                     "type":"api",
                     "format":"json",
                     "url":"http://my.api.com/",
                     "extra":{
                        "idClient":"{{idClient}}"
                     },
                     "max_threads":"",
                     "err_node_id":"52fa3b7a10e87b098d49aba2"
                  },
                  {
                     "type":"go",
                     "format":"json",
                     "to_node_id":"52f4e08810e87b098dba2f1b",
                     "node_title":"Нашли клиента?"
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
               "title":"Выход",
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
               "title":"Нашли клиента в ЕКБ по телефону?",
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
               "title":"Ошибка ЕКБ",
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
               "title":"Старт",
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

Где в каждом элеменете `"obj":"node"` есть параметр `count` - текущее количество заявок в узле.

## Получение статистики по ID диаграммы и узла за период

Входящие параметры:
*   type - тип show
*   obj - stat
*   conv_id - ID процесса
*   start - период "с" в формате UNIX
*   end - период "по" в формате UNIX
*   interval - за какие интервалы будет предоставлена статистика
    *   day - в разрезе дней
    *   hour - в разрезе часов
    *   minute - в разрезе минут
*   group -
*   node_id - ID узла

**Запрос:**
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

**Ответ:**
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
