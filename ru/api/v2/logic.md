# Добавление логик

*   [Создание узлов для добавления логик API Call, Code, Copy task, Modify Task, Call Process, Get from Queue](#создание-узлов-для-добавления-логик-api-call-code-copy-task-modify-task-call-process-get-from-queue)
*   [Добавление Логики API Call](#добавление-логики-api-call)
*   [Добавление Логики Condition](#добавление-логики-condition)
*   [Добавление Логики Sum](#добавление-логики-sum)

## Создание узлов для добавления логик API Call, Code, Copy task, Modify Task, Call Process, Get from Queue

Для добавления указанных логик необходимо создать сразу 4 узла:

* **обычный узел** (тип 0) - для основной логики
* **эскалационный узел** (тип 3) - для Логики Condition, чтобы распределить ошибки основной логики по процессу - в финальный узел или на повтор обработки
* **обычный узел** (тип 0) - для Логики Delay, чтобы обрабатывать ошибки основной логики, которые можно повторить через 30 сек
* **финальный узел** (тип 2) - для ошибок основной логики, которые нельзя обработать повторно

**Пример запроса** создания узлов для добавления Логики API Call в процесс 125892

```json
{
  "ops": [
    {
      "id": "1",
      "type": "create",
      "obj": "node",
      "conv_id": 125892,
      "title": "API Call",
      "description": "",
      "obj_type": 0,
      "version": 1487321422
    },
    {
      "id": "2",
      "type": "create",
      "obj": "node",
      "conv_id": 125892,
      "title": "Escalation node for API Call",
      "description": "",
      "obj_type": 3,
      "version": 1487321422
    },
    {
      "id": "3",
      "type": "create",
      "obj": "node",
      "conv_id": 125892,
      "title": "Delay for API Call",
      "description": "",
      "obj_type": 0,
      "version": 1487321422
    },
    {
      "id": "4",
      "type": "create",
      "obj": "node",
      "conv_id": 125892,
      "title": "Final errors for API Call",
      "description": "",
      "obj_type": 2,
      "version": 1487321422
    }
  ]
}
```

**Ответ**
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "1",
      "proc": "ok",
      "obj": "node",
      "obj_id": "963852",
      "version": 1487321422
    },
    {
      "id": "2",
      "proc": "ok",
      "obj": "node",
      "obj_id": "741852",
      "version": 1487321422
    },
    {
      "id": "3",
      "proc": "ok",
      "obj": "node",
      "obj_id": "852123",
      "version": 1487321422
    },
    {
      "id": "4",
      "proc": "ok",
      "obj": "node",
      "obj_id": "632547",
      "version": 1487321422
    }
  ]
}
```
## Добавление Логики API Call

**Пример запроса** добавления Логики API Call в процесс 125892

С параметрами вызываемого API:

* тип запроса - POST
* URL API - https://test.com
* входящие параметры - {"key1": "value1", "key2": "2"}
* Content-Type - Application/Json

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{logic_node_id}}",
      "conv_id": 125892,
      "title": "",
      "description": "",
      "obj_type": 0,
      "logics": [
        {
          "type": "api",
          "err_node_id": "{{escalation_node_id}}",
          "format": "",
          "method": "POST",
          "url": "https:\/\/test.com",
          "extra": {
            "key1": "value1",
            "key2": "2"
          },
          "extra_type": {
            "key1": "string",
            "key2": "number"
          },
          "max_threads": 5,
          "debug_info": false,
          "customize_response": false,
          "response": {
            "header": "{{header}}",
            "body": "{{body}}"
          },
          "response_type": {
            "header": "object",
            "body": "object"
          },
          "extra_headers": {

          },
          "send_sys": true,
          "cert_pem": "",
          "content_type": "application\/json"
        },
        {
          "type": "go",
          "to_node_id": "{{final_node_id}}"
        }
      ],
      "semaphors": [

      ],
      "position": [
        -1680,
        -100
      ],
      "extra": {
        "modeForm": "expand",
        "icon": ""
      },
      "version": 1487321422
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{escalation_node_id}}",
      "conv_id": 125892,
      "title": "",
      "description": "",
      "obj_type": 3,
      "logics": [
        {
          "type": "go_if_const",
          "to_node_id": "{{delay_node_id}}",
          "conditions": [
            {
              "fun": "eq",
              "const": "hardware",
              "param": "__conveyor_api_return_type_error__",
              "cast": "string"
            }
          ]
        },
        {
          "type": "go_if_const",
          "to_node_id": "{{delay_node_id}}",
          "conditions": [
            {
              "fun": "eq",
              "const": "software",
              "param": "__conveyor_api_return_type_error__",
              "cast": "string"
            },
            {
              "fun": "eq",
              "const": "api_bad_answer",
              "param": "__conveyor_api_return_type_tag__",
              "cast": "string"
            }
          ]
        },
        {
          "type": "go",
          "to_node_id": "{{final_node_id}}"
        }
      ],
      "semaphors": [

      ],
      "position": [
        -1428,
        -8
      ],
      "extra": {
        "modeForm": "collapse",
        "icon": ""
      },
      "version": 1487321422
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{delay_node_id}}",
      "conv_id": 125892,
      "title": "",
      "description": "",
      "obj_type": 0,
      "logics": [

      ],
      "semaphors": [
        {
          "type": "time",
          "value": 30,
          "dimension": "sec",
          "to_node_id": "{{logic_node_id}}"
        }
      ],
      "position": [
        -1428,
        -100
      ],
      "extra": {
        "modeForm": "collapse",
        "icon": ""
      },
      "version": 1487321422
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{final_node_id}}",
      "conv_id": 125892,
      "title": "",
      "description": "",
      "obj_type": 2,
      "logics": [

      ],
      "semaphors": [

      ],
      "position": [
        -1296,
        20
      ],
      "extra": {
        "modeForm": "collapse",
        "icon": "error"
      },
      "version": 1487321422
    }
  ]
}
```

| parameter | accept type | description | required |
| -- | -- | -- | -- |
| logic_node_id | string | id узла, созданного для Логики API Call | + |
| escalation_node_id | string | id эскалационного узла Логики API Call | + |
| delay_node_id | string | id узла, созданного для Логики Delay | + |
| final_node_id | string | id финального узла, созданного для архива ошибок Логики API Call | + |


**Ответ**
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "proc": "ok",
      "conv_id": 125892,
      "obj_id": "{{logic_node_id}}"
    },
    {
      "id": "",
      "proc": "ok",
      "conv_id": 125892,
      "obj_id": "{{escalation_node_id}}"
    },
    {
      "id": "",
      "proc": "ok",
      "conv_id": 125892,
      "obj_id": "{{delay_node_id}}"
    },
    {
      "id": "",
      "proc": "ok",
      "conv_id": 125892,
      "obj_id": "{{final_node_id}}"
    }
  ]
}
```
## Добавление Логики Condition

**Запрос**

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{node_id}}",
      "conv_id": {{conv_id}},
      "title": "{{title}}",
      "description": "",
      "obj_type": 0,
      "logics": [
        {
          "to_node_id": "{{condition_ok_node_id}}",
          "type": "go_if_const",
          "id": "{{request_id}}",
          "conditions": [
            {
              "param": "{{key}}",
              "const": "{{value}}",
              "fun": "{{fun}}",
              "cast": "{{key_type}}"
            }
          ]
        },
        {
          "type": "go",
          "to_node_id": "{{go_node_id}}"
        }
      ],
      "semaphors": [

      ],
      "position": [
        {{position_X}},
        {{position_Y}}
      ],
      "extra": {
        "modeForm": "expand",
        "icon": ""
      },
      "version": {{version}}
    }
  ]
}
```

| parameter | accept type | description | required |
| -- | -- | -- | -- |
| node_id | string | id узла | + |
| conv_id | string / number | id процесса | + |
| title | string (240) | Заголовок создаваемого узла | - |
| condition_ok_node_id | string | id узла для перехода, если указанное условие выполнено | + |
| request_id | string | id запроса | - |
| key | string | Ключ условия | + |
| value | string | Значение условия. Может быть динамическим из тела заявки {{data.param1}} и пустым "" | + |
| fun | string | Тип условия ("eq", "not_eq", "more", "less", "regexp") | + |
| key_type | string | Тип ключа ("string", "number", "boolean", "array","object") | + |
| go_node_id | string | id узла для безусловного перехода, если ни одно из указанных условий не выполнено | + |
| position_X | number | Координаты левого верхнего угла узла по оси X, относительно условной точки 0:0 координат поля процесса | + |
| position_Y | number | Координаты левого верхнего угла узла по оси Y, относительно условной точки 0:0 координат поля процесса | + |
| version | number | Версия (идентификатор) изменений | + |

**Пример запроса** добавления Логики Condition с двумя условиями:

1) если параметр `amount` больше 100 (число) и параметр `card` не пустой (присутсвует в заявке), то переход в узел с id 8523069879
2) если параметр `amount` равен 0 (число), то переход в узел с id 1485269578
3) если не выполнено ни одно из указанных условий, переход в узел с id 8547963253

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "1235809652",
      "conv_id": 125892,
      "title": "",
      "description": "",
      "obj_type": 0,
      "logics": [
        {
          "to_node_id": "8523069879",
          "type": "go_if_const",
          "id": "1",
          "conditions": [
            {
              "param": "amount",
              "const": "100",
              "fun": "more",
              "cast": "number"
            },
            {
              "param": "card",
              "const": "",
              "fun": "not_eq",
              "cast": "string"
            }
          ]
        },
        {
          "to_node_id": "1485269578"
          "id": "2",
          "type": "go_if_const",
          "conditions": [
            {
              "param": "amount",
              "const": "0",
              "fun": "eq",
              "cast": "number"
            }
          ]
        },
        {
          "type": "go",
          "to_node_id": "8547963253"
        }
      ],
      "semaphors": [

      ],
      "position": [
        -2604,
        -276
      ],
      "extra": {
        "modeForm": "expand",
        "icon": ""
      },
      "version": 1487234301
    }
  ]
}
```

## Добавление Логики Sum

**Запрос**

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "{{node_id}}",
      "conv_id": {{conv_id}},
      "title": "{{title}}",
      "description": "",
      "obj_type": 0,
      "logics": [
        {
          "type": "api_sum",
          "extra": [
            {
              "id": "{{request_id}}",
              "name": "{{name}}",
              "value": "{{value}}"
            }
          ]
        },
        {
          "type": "go",
          "to_node_id": "{{go_node_id}}"
        }
      ],
      "semaphors": [

      ],
      "position": [
        {{position_X}},
        {{position_Y}}
      ],
      "extra": {
        "modeForm": "expand",
        "icon": ""
      },
      "version": {{version}}
    }
  ]
}
```

| parameter | accept type | description | required |
| -- | -- | -- | -- |
| node_id | string | id узла | + |
| conv_id | string / number | id процесса | + |
| title | string (240) | Заголовок создаваемого узла | - |
| request_id | string | id запроса (id суммы параметров). Может быть использован в конструкции https://doc.corezoid.com/ru/interface/functions/getParamFromCount.html | + |
| name | string | Имя параметра, который будет содержать сумму значений | + |
| value | string | константа или имя параметра из заявки в двойных фигурных скобках, значение которого нужно суммировать | + |
| go_node_id | string | id узла следующего узла | + |
| position_X | number | Координаты левого верхнего угла узла по оси X, относительно условной точки 0:0 координат поля процесса | + |
| position_Y | number | Координаты левого верхнего угла узла по оси Y, относительно условной точки 0:0 координат поля процесса | + |
| version | number | Версия (идентификатор) изменений | + |

**Пример запроса** добавления Логики Sum для суммирования параметра `amount` по заявкам процесса 125892

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "123589635",
      "conv_id": 125892,
      "title": "SUM",
      "description": "",
      "obj_type": 0,
      "logics": [
        {
          "type": "api_sum",
          "extra": [
            {
              "id": "1",
              "name": "Total amount",
              "value": "{{amount}}"
            }
          ]
        },
        {
          "type": "go",
          "to_node_id": "85236954"
        }
      ],
      "semaphors": [

      ],
      "position": [
        716,
        188
      ],
      "extra": {
        "modeForm": "expand",
        "icon": ""
      },
      "version": 1487582372
    }
  ]
}
```
