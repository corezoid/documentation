# Описание протокола

Чтобы сформировать запрос, создайте `API keys` и получите **логин авторизации** и **секретный ключ** для работы с объектами Corezoid через API

`Users -> Create -> API key -> Введите название -> OK`

![](../img/create_api_keys.gif)


**URL**

```
https://api.corezoid.com/api/2/json/{API_LOGIN}/{GMT_UNIXTIME}/{SIGNATURE}
```

*   **{API_LOGIN}** - логин авторизации

*   **{GMT_UNIXTIME}** - время запроса, в формате unix time в секундах (epoch time), по Гринвичу (GMT+0).

*   **{SIGNATURE}** - подпись запроса.

Подпись запроса расчитывается по формуле:

`hex( sha1({GMT_UNIXTIME} + {API_SECRET} + {CONTENT} + {API_SECRET}) )`, где


    *   `hex()` - функция, которая приводит бинарные данные к шестнадцатеричному формату
    *   `sha1()` - стандартная хеш-функция SHA-1, должна возвращать бинарные данные
    *   `{GMT_UNIXTIME}` - время запроса, в формате unix time в секундах (epoch time), по Гринвичу (GMT+0)
    *   `+` -  конкатенация текстовой строки
    *   `{API_SECRET}` - секретный ключ который выдается вместе с логином `{API_LOGIN}`
    *   `{CONTENT}` - тело запроса

Весь запрос находится в http-теле (он же `{CONTENT}` в формуле подписи).

Кодировка текста `utf-8`. Это полностью соответствует стандарту, и посылается вместе со следующим http заголовком в json формате:

`Content-type: application/json; charset=utf8`

**Запрос**

Отправляется массив **ops**, который содержит список операций. Например:
```json
{
  "ops": [
    {
      "type": "create",
      "obj": "conv"
    },
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "n1234"
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
      "obj": "conv",
      "obj_id": "1234",
      "proc": "ok"
    },
    {
      "obj": "node",
      "obj_id": "n1234",
      "proc": "obj_id_not_found"
    }
  ]
}
```

| parameter | value | description |
| -- | -- | -- |
| request_proc | "ok" в случае успешного выполнения, иначе - ошибка | глобальный статус обработки всего пакета |
| ops | [] | список операций, соответствующий списку операций запроса |
| ops[n].proc | "ok" в случае успешного выполнения, иначе - ошибка | статус обработки конкретной операции |


Пример ошибки всего пакета:
```json
{
  "request_proc": "format_error",
  "ops": [

  ]
}
```

В этом случае список операций в ответе пуст поскольку ни одна из операций запроса не была выполнена.
