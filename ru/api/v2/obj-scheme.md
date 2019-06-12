# Получение объектов

Метод можно использовать для получения содержимого объектов используя API, идентичного ручной выгрузке объекта в файл с платформ Corezoid.

Все содержимое массива `scheme: []`, можно сохранить в файл с расширением json и в дальнейшем использовать для загрузки объектов в Corezoid через интерфейс.

**Запрос**

```json
{
    "ops": [
        {
            "type": "get",
            "obj": "obj_scheme",
            "obj_id": 4740,
            "obj_type": "conv",
            "async": false
        }
    ]
}
```

| parameter | description |
| --- | --- |
| obj_id | идентификатор объекта |
| obj_type |тип объекта conv / folder / dashboard |
| async | выбор режима получения объекта true / false |

**Ответ**

```json
{
    "request_proc": "ok",
    "ops": [
        {
            "id": "",
            "obj": "obj_scheme",
            "proc": "ok",
            "scheme": [
                {
                    "obj_type": 1,
                    "obj_id": 4740,
                    "parent_id": 0,
                    "title": "fol_get_obj_scheme",
                    "description": "fol_get_obj_scheme",
                    "status": "actived",
                    "params": null,
                    "conv_type": "process",
                    "scheme": {
                        "nodes": [
                            {
                                "id": "58134741e44b60791c00199e",
                                "obj_type": 2,
                                "condition": {
                                    "logics": [],
                                    "semaphors": []
                                },
                                "title": "Final",
                                "description": "",
                                "x": 988,
                                "y": 400,
                                "extra": "{\"modeForm\":\"collapse\",\"icon\":\"error\"}"
                            },
                            {
                                "id": "58134741e44b60791c00199f",
                                "obj_type": 1,
                                "condition": {
                                    "logics": [
                                        {
                                            "type": "go",
                                            "to_node_id": "58134741e44b60791c00199e"
                                        }
                                    ],
                                    "semaphors": []
                                },
                                "title": "Start",
                                "description": "",
                                "x": 988,
                                "y": 100,
                                "extra": "{\"modeForm\":\"collapse\",\"icon\":\"\"}"
                            }
                        ],
                        "web_settings": [
                            [],
                            []
                        ]
                    },
                    "company_id": null
                }
            ]
        }
    ]
}
```

**Массив данных, которые можно сохранить в файл json**

```json
[
                {
                    "obj_type": 1,
                    "obj_id": 4740,
                    "parent_id": 0,
                    "title": "fol_get_obj_scheme",
                    "description": "fol_get_obj_scheme",
                    "status": "actived",
                    "params": null,
                    "conv_type": "process",
                    "scheme": {
                        "nodes": [
                            {
                                "id": "58134741e44b60791c00199e",
                                "obj_type": 2,
                                "condition": {
                                    "logics": [],
                                    "semaphors": []
                                },
                                "title": "Final",
                                "description": "",
                                "x": 988,
                                "y": 400,
                                "extra": "{\"modeForm\":\"collapse\",\"icon\":\"error\"}"
                            },
                            {
                                "id": "58134741e44b60791c00199f",
                                "obj_type": 1,
                                "condition": {
                                    "logics": [
                                        {
                                            "type": "go",
                                            "to_node_id": "58134741e44b60791c00199e"
                                        }
                                    ],
                                    "semaphors": []
                                },
                                "title": "Start",
                                "description": "",
                                "x": 988,
                                "y": 100,
                                "extra": "{\"modeForm\":\"collapse\",\"icon\":\"\"}"
                            }
                        ],
                        "web_settings": [
                            [],
                            []
                        ]
```
