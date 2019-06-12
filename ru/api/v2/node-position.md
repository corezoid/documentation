# Установка координат узла

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
      "obj_type": {{obj_type}},
      "description": "{{description}}",
      "logics": [

      ],
      "semaphors": [

      ],
      "position": [
        {{position_X}},
        {{position_Y}}
      ],
      "extra": {
        "modeForm": "{{modeForm}}",
        "icon": "{{icon}}"
      },
      "version": {{version}}
    }
  ]
}
```

| parameter | accept type | description | required |
| --- | --- | --- | --- |
| node_id | string | id созданного узла | + |
| conv_id | string / number | id процесса | + |
| title | string (240) | Заголовок создаваемого узла | - |
| obj_type | number | Тип узла | + |
| description | string (2000) | Описание создаваемого узла | - |
| position_X | number | Координаты левого верхнего угла узла по оси X, относительно условной точки 0:0 координат поля процесса | + |
| position_Y | number | Координаты левого верхнего угла узла по оси Y, относительно условной точки 0:0 координат поля процесса | + |
| modeForm | string | Режим узла `collapse` (свернут) / `expand` (развернут) | + |
| icon | string | Для финального узла `success` (зеленый) / `error` (красный). Для всех остальных - "icon":"" | + |
| version | number | Версия (идентификатор) изменений | + |

**Пример запроса** установки координат финального узла в процессе 125892

```json
{
  "ops": [
    {
      "type": "modify",
      "obj": "node",
      "obj_id": "741852963",
      "conv_id": 125892,
      "title": "Final",
      "obj_type": 2,
      "description": "",
      "logics": [

      ],
      "semaphors": [

      ],
      "position": [
        -1580,
        160
      ],
      "extra": {
        "modeForm": "collapse",
        "icon": "success"
      },
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
      "id": "",
      "proc": "ok",
      "conv_id": 125892,
      "obj_id": "741852963"
    }
  ]
}
```
