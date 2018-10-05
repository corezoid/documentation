# Заявки (Tasks)
Заявка - это текстовый файл в формате JSON. Информация в таком файле содержится в формате `"параметр":"значение"`.

Пример заявки:

```json
{
        "create_time": "2015.11.10 18:13:29",
        "change_time": "2015.11.10 18:13:29",
        "node_prev_id": null,
        "status": "created",
        "user_id": 001,
        "data": {
                "message": {
                        "nick": "Vitaliy",
                        "message": "Hello, world!",
                }
        }
}
```

Каждая заявка состоит из служебной информации (`create_time`, `change_time`, `node_prev_id`, `status`, `user_id`) и, собственно, данных, которые мы можем анализировать и изменять по ходу процесса (`data`).

###Доступ к параметрам заявки

Доступ к содержимому параметра `nick` этой заявки имеет следующий синтаксис: `{{message.nick}}`.

**Максимальный размер заявки - 128 КБ**

В случае его превышения, к заявке добавятся новые параметры и она попадет в узел ошибкой.

| Имя параметра | Значение |
| -- | -- |
| `__conveyor_api_return_type_error__` | software |
| `__conveyor_api_return_type_tag__` | api_task_size_overflow_limit |
| `__conveyor_api_return_description__` | Your task size: {{size_data}} bytes, Max available task size: 128000 bytes, Try to change your data or try to split your task ... |

