# Создание объектов (процесс, папка, дашборд)

## Запрос
```json
{
  "ops": [
    {
      "title": "{{title}}",
      "description": "{{description}}",
      "folder_id": "{{folder_id}}",
      "company_id": "{{company_id}}",
      "obj": "{{obj}}",
      "type": "create",
      "obj_type": 0,
      "conv_type": "{{conv_type}}",
      "create_mode": "without_nodes",
      "status": "{{status}}"
    }
  ]
}
```

| parameter | accept type | description | required |
| -- | -- | -- | -- |
| `title` | string | Название объекта | `+` |
| `description` | string  / null | Текстовое описание объекта | `+` |
| `folder_id` | string / number | Идентификатор папки, в которой будет создан объект | `-` |
| `company_id` | string  / null | Идентификатор компании, в которой будет создан объект (если нет компании, параметр не передается или имеет значение null) | `-` |
| `obj` | string | Тип объекта. Принимаются значения `conv / folder / dashboard` | `+` |
| `conv_type` | string | Принимаются значения `process` - процесс / `state` - диаграмма состояний | `+` только для "obj": "conv" |
| `status` | string | Статус процесса. Принимает значения `actived / paused / debugged` | `+` |

### Пример запроса

создания активного процесса с названием "Corezoid" в папке 11456 компании i7856235891

```json
{
  "ops": [
    {
      "title": "Corezoid",
      "description": null,
      "folder_id": 11456,
      "company_id": "i7856235891",
      "obj": "conv",
      "type": "create",
      "obj_type": 0,
      "conv_type": "process",
      "create_mode": "without_nodes",
      "status": "actived"
    }
  ]
}
```

## Ответ
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "",
      "proc": "ok",
      "obj": "conv",
      "obj_id": 24545,
      "folder_id": 11456,
      "hash": "ce48cf53644b20ee6ce6e936f271a4f893a29298"
    }
  ]
}
```

| parameter | description |
| -- | -- |
| `obj` | Тип созданного объекта `conv / folder / dashboard` |
| `obj_id` | Идентификатор созданного объекта |
| `folder_id` | Идентификатор папки, в которой создан объект |
| `hash` | Ключ объекта для формирования "Direct url for tasks upload" |
