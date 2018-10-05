# Узлы диаграммы

*   [Добавление узла](#добавление-узла)
*   [Получение списка узлов](#получение-списка-узлов)
*   [Удаление узла](#удаление-узла)

## Добавление узла

Создадим сразу несколько узлов в одном процессе.

Запрос:
```json
{
  "ops": [
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Узел обработки",
      "description": "Это стартовый узел …",
      "obj_type": "1"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Конечный узел, удача",
      "obj_type": "2"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Узел эскалации",
      "obj_type": "3"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Конечный узел, ошибка",
      "obj_type": "2"
    },
    {
      "type": "create",
      "obj": "node",
      "conv_id": "1234",
      "title": "Узел эскалации, конец",
      "obj_type": "2"
    }
  ]
}
```

`obj_type` определяет тип узла:
*   0 - обычный
*   1 - стартовый (в одном процессе может быть только один стартовый узел)
*   2 - конечный
*   3 - эскалационный

Ответ при успешном выполнении операции:
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

## Получение списка узлов

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
                     "max_theads":"",
                     "err_node_id":"52fa3b7a10e87b098d49aba2"
                  },
                  {
                     "type":"go",
                     "format":"json",
                     "to_node_id":"52f4e08810e87b098dba2f1b",
                     "node_title":"Нашли клиента?"
                  }
               ],
               "semaphors":[

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
## Удаление узла

Запрос
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

Ответ если процесс не найден:
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
