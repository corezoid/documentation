# Логика процесса

*   [Добавление логики](#добавление-логики)
*   [Управление логикой](#управление-логикой)
*   [Удаление логики](#удаление-логики)

## Добавление логики

Добавим в "Узел обработки" (node_id="n10221") логику:
*   когда количество задач в узле превысит 1000, создаем эскалацию (параллельно) в узле "Узел эскалации" (node_id="n10233").
*   логика по времени 10 минут (600 секунд). Когда задача в узле находится больше этого времени, она переходит в "Конечный узел, ошибка" (node_id="n10234").

Запрос:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Ошибка ЕКБ",
      "obj_type": 3,
      "semaphors": [
        {
          "type": "count",
          "value": "1000",
          "esc_node_id": "n10233"
        },
        {
          "type": "time",
          "value": "600",
          "to_node_id": "n10234"
        }
      ]
    }
  ]
}
```

Ответ при удачном выполнении операции:
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

### RPC

```json
{
  "type": "api_rpc",
  "conv_id": 1,
  "extra": {
    "param1":"value"
  },
  "err_node_id": ""
}
```

### RPC reply

Два варианта настройки:
```json
{
  "type": "api_rpc_reply",
  "mode": "keys",
  "res_data": [
    "key1",
    "key2",
    "key3"
  ]
}
```

```json
{
  "type": "api_rpc_reply",
  "mode": "key_value",
  "res_data": {
    "key1":"value1",
    "key2":"value2",
    "key3":"value3",
  }
}
```

## Управление логикой

"Узел обработки" (node_id="n10221").

Добавим в "Узел обработки" (node_id="n10221"):
1.  Вызов стандартного API (его нам пришлет параметр res) на URL: http://my_api.com/?f=json в формате json.
2.  Если параметр "res" равен "0", переходим в "Конечный узел, удача" (node_id="n10222").
3.  Иначе - переходим в "Конечный узел, ошибка" (node_id="n10234").

Запрос:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Ошибка ЕКБ",
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

Ответ при удачном выполнении операции:
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


## Удаление логики

Удаление производится удалением узла из JSON и отправкой запроса с параметрами:
*   `type` = `modify`
*   `obj` = `node`

Запрос до удаления логики:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Ошибка ЕКБ",
      "obj_type": 3,
      "logics": [
        {
          "type": "api",
          "format": "json",
          "url": "http://my_api.com/?f=json"
        },
        /// удаляем этот блок логики =======
        {
          "type": "go_if_const",
          "param": "res",
          "fun": "eq",
          "const": "0",
          "to_node_id": "n10222"
        },
        ///=================================
        {
          "type": "go",
          "to_node_id": "n10234"
        }
      ]
    }
  ]
}
```

Запрос после удаления логики, готовый к отправке:
```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n10221",
      "conv_id": "1234",
      "title": "Ошибка ЕКБ",
      "obj_type": 3,
      "logics": [
        {
          "type": "api",
          "format": "json",
          "url": "http://my_api.com/?f=json"
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
