# Копирование папки в компанию

[Шаблон процесса](https://admin.corezoid.com/folder/conv/103787) для копирования в свой аккаунт.

>В примере предполагается, что:

* в копируемой папке расположен процесс и дашборд

* новую папку, процесс и дашборд нужно переименовать (например, назвать именем клиента)

* вызывающему процессу нужно вернуть id процесса, расположенного в новой папке

## Описание параметров

* `login` - логин юзера с типом API
* `secret_key` - ключ юзера с типом API******
* `copy_folder_id` - id копируемой папки
* `company_id` - id компании, куда нужно скопировать папку.

Если копия папки нужна в "MY COREZOID", значение company_id = **null**
* `to_folder_id` - папка, куда нужно скопировать папку
* `folder_new_name` - имя новой папки
* `dashboard_new_name` - имя нового дашборда
* `process_new_name` - имя нового процесса

Параметры `folder_new_name`, `dashboard_new_name`, `process_new_name` могут быть заменены на другие параметры текущей завки.

Например,

"{{folder_new_name}}" -> "{{public_key}}"

"{{dashboard_new_name}}" -> "Dashboard-{{public_key}}"

"{{process_new_name}}" -> "Process-{{public_key}}"


>****** `secret_key` необходимо добавить в каждый узел с вызовом API Corezoid:

>Additionally -> Sign the request by secret key

![](img/secret_key.png)
