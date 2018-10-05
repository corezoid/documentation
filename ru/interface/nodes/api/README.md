# Логика API Call

Возможна интеграция с любым API в форматах:
*   JSON
*   XML
*   SOAP

![](../../img/create/api_call.png)

Узлы, которые на рисунке обведены серым квадратом, добавляются автоматически для обработки ошибок, возникающих при вызове API.

## URL API

![](../../img/create/api_call_URL_API.png)


**URL** - URL API

**Request format** - формат запроса
* `Corezoid` - запрос к API в [формате corezoid](corezoid.md)
* `Default` - дает возможность выбрать HTTP метод запроса к API

**Request method** - [GET](get.md), [POST](post.md), [PUT, DELETE, HEAD, PATCH](put__delete__head.md)

**Content-Type** - определяет вид запроса к API:
*   application/json
*   application/x-www-form-urlencoded
*   application/xml
*   text/xml
*   application/soap+xml


## Parameters

#### Key-Value

![](../../img/create/api_call_parameters.png)


**`Key`** (имя параметра) = **`Value`** (значение параметра)

**`+ Add "key-value"`** - кнопка добавления новой пары key-value

`Value` может содержать:
- константу
- `{{имя_параметра}}` из заявки, значение которого будет вставлено. Если параметр содержит массив или имя параметра неправильно указано - будет вставлена пустая строка
-   `{{root.task_id}}` - id заявки, генерирует сам процесс
-   `{{root.ref}}` - референс заявки
-   `{{root.conv_id}}` - id процесса
-   `{{root.node_id}}` - id узла
-   `{{root.prev_node_id}}` - id предыдущего узла
-   `{{root.create_time}}` - время создания заявки unixtime
-   `{{root.change_time}}` - время изменения заявки unixtime
-   `{{root.end_time}}` - динамическое время срабатывания таймера (например если нужно в 8 часов утра чтобы таймер сработал)
-   `{{root.user_id}}` - ID пользователя, который последний менял заявку


#### Code editor

![](../../img/create/api_call_parameters_code_editor.png)

Добавление параметров запросов в формате JSON

![](../../img/create/editor_code.png)


## Additionally

#### Header parameters

![](../../img/create/api_call_header.png)

Добавление в Header HTTP запроса параметров в формате "key-value"

#### Customize response parameters

Позволяет получить доступ к параметрам ответа `header` и `body`

![](../../img/create/api_call_customize.png)

**Response format** - определяет вид ответа от API:
*   Default
*   application/json
*   application/x-www-form-urlencoded
*   application/xml
*   text/xml
*   application/soap+xml

**`+ Add "key-value"`** - добавить другие параметры из ответа

#### Limit the number of simultaneous requests to the API

![](../../img/create/api_call_threads.png)

Максимальное количество одновременных запросов к API.

По умолчанию = 5.


#### Send system parameters

Наличие данного флага добавляет системыне параметры в URL запроса.

![](../../img/create/api_call_send_sys.png)

Например,

http://api.openweathermap.org/data/2.5/weather?q=london&units=metric&conv_signature={{conv_signature}}&conv_time={{conv_time}}&conv_id={{conv_id}}

`conv_signature` - ключ, который сгенерирован в узле с логикой API. Является уникальным значением и формируется по правилам, опсанным в разделе "[Описание протокола](../../../api/spec.md)".

`conv_time` - время запроса, в формате unix time в секундах (epoch time), по Гринвичу (GMT+0), целое число, обязательный параметр.

`conv_id` - id процесса.


#### Debug info

![](../../img/create/api_call_debug.png)

Включение флага добавляет в заявку время выполнения http запроса к API в миллисекундах.
Это значение содержит параметр `{{__conveyor_api_debug__.http_exec_time}}`
Параметр `{{__conveyor_api_debug__.http_res_code}}` содержит HTTP status code.

#### Sign the request by secret key

![](../../img/create/api_call_sign_request.png)

Включение флага добавляет ключ, которым будет подписан запрос к API при формировании [сигнатуры](../../../api/spec.md).


#### Sign the request by certificate

![](../../img/create/api_call_srtificate.png)

Добавление в вызов API персонального сертификата. Формат:
```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
....
-----END CERTIFICATE-----
```


#### Alert when there is tasks queue

Критическое количество заявок в узле.

Подробное [описание](../timer.md#tasks-limit) логики работы.

#### Limit the time of the task in the node

Значение временного интервала, при достижении которого заявка пойдет дальше по процессу в том случае, если Логика API Call не отвечает.

Подробное [описание](../timer.md#timer) логики работы.
