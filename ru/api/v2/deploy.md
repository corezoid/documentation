# Deploy процесса

**Запрос**

```json
{
  "ops": [
    {
      "type": "confirm",
      "obj": "commit",
      "conv_id": {{conv_id}},
      "company_id": {{company_id}},
      "version": {{version}}
    }
  ]
}
```

| parameter | accept type | description | required |
| --- | --- | --- | --- |
| conv_id | string / number | id процесса | + |
| company_id | string  / null | Идентификатор компании. Если нет компании, параметр не передается или имеет значение null | - |
| version | number | Версия (идентификатор) изменений | + |

**Пример запроса** на Deploy процесса 125892

```json
{
  "ops": [
    {
      "type": "confirm",
      "obj": "commit",
      "conv_id": 125892,
      "company_id": null,
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
      "version": 1487321422
    }
  ]
}
```
