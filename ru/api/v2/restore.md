
## Восстановление объекта

Метод для восстановления удаленного объекта Corezoid из корзины.

**URL**

```
https://api.corezoid.com/api/2/download/{API_LOGIN}/{GMT_UNIXTIME}/{SIGNATURE}
```

**Запрос**

```json
{
    "ops": [
        {
            "type": "restore",
            "obj": "conv",
            "obj_id": 480063
        }
    ]
}
```

| parameter | description |
| --- | --- |
| obj_id | идентификатор объекта |
| obj_type |тип объекта conv / folder / dashboard |

**Ответ**

```json
{
    "ops": [
        {
            "id":"",
            "obj":"conv",
            "obj_id":480063,
            "parent_folder_id":0,
            "proc": "ok"
        }
    ],
    "request_proc": "ok"
}
```

Параметр `parent_folder_id` - ID папки, в которую восстановлен объект (0 - в корень компании).

Если в корзине нет объекта с указанным ID, ответ будет содержать ошибку "Deleted object <obj> with id <obj_id> does not exist".