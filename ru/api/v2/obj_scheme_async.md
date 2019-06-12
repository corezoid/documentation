# Выгрузка объектов

Метод идентичный ручной выгрузке объекта Corezoid в файл.

**URL**

```
https://api.corezoid.com/api/2/download/{API_LOGIN}/{GMT_UNIXTIME}/{SIGNATURE}
```

**Запрос**

```json
{
    "ops": [
        {
            "obj": "obj_scheme",
            "obj_id": 236739,
            "obj_type": "folder",
            "async": true
        }
    ]
}
```

| parameter | description |
| --- | --- |
| obj_id | идентификатор объекта |
| obj_type |тип объекта conv / folder / dashboard |
| async | выбор режима получения объекта true / false , true - возвращает ссылку на файл .json, false - возвращает  JSON схему объекта |

**Ответ**

Для `"async": true`:

```json
{
    "ops": [
        {
            "download_url": "https://www.corezoid.com/user_downloads/folder_236739_1540473741.json",
            "obj": "obj_scheme",
            "proc": "ok"
        }
    ],
    "request_proc": "ok"
}
```

Для `"async": false` ответ будет таким же, как на запрос для [получения объектов](#получение-объектов)
