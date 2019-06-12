# Object creation

**Request**

```json
{
  "ops": [
    {
      "id": "{{request_id}}",
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
| --- | --- | --- | --- |
| request_id | string | Request id | - |
| title | string | Object title | + |
| description | string  / null | Description | + |
| folder_id | string / number | ID of the folder in which the object will be created | - |
| company_id | string  / null | Company ID (for **My Corezoid** parameter may be missing or null) | - |
| obj | string | Object type, possible values: `conv / folder / dashboard` | + |
| conv_type | string | Possible values: `process` or / `state` - state diagram | `+` only for "obj": "conv" |
| status | string | Process status. Possible values: `actived / paused / debugged` | + |

**Request**

For creating active process with title "Corezoid" in folder 11456 of company i7856235891

```json
{
  "ops": [
    {
      "id": "147",
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

**Response**
```json
{
  "request_proc": "ok",
  "ops": [
    {
      "id": "147",
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
| --- | --- |
| id | request id |
| obj | Type of created object, possible values: `conv / folder / dashboard` |
| obj_id | ID of created object |
| folder_id | Folder ID |
| hash | Hash to make "Direct url for tasks upload" |