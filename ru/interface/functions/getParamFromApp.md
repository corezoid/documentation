# Получение значений параметров заявки

С помощью CONV можно получить из диаграммы всю заявку:

`{{conv[{{diag_id}}].ref[{{ref}}]}}`

или значение параметра из заявки:

`{{conv[{{diag_id}}].ref[{{ref}}].param}}`

Из процесса или архивного узла прочитать данные невозможно.

Пример:

    //возвращает всю заявку с REF = menu из диаграммы с ID = 123456 (необходимо указать тип параметра Object)

    {{conv[123456].ref[menu]}}

    // возвращает значение параметра amount из заявки с REF = qwerty диаграммы с ID = 123456

    {{conv[123456].ref[qwerty].amount}}

    // возвращает значение из заявки с REF = {{ref}} и диаграммы с ID = {{diag_id}}

        {{conv[{{diag_id}}].ref[{{ref}}].ID_параметра}}

При использовании CONV выполняются **проверки**:
* что указан ID диаграммы состояний, а не процесса
* диаграмма состояний не удалена
* есть доступ к указанной диаграмме состояний

### Типы ошибок

Здесь описаны ошибки, которые возникают при использовании CONV в логике Set Parameter.

#### Некорректный тип параметра или параметр в указанной заявке отсутствует

| Имя параметра | Значение |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | set_param_wrong_convert_param |
| __conveyor_set_param_return_description__ | Param: `{{param}}`, Value: `{{value}}`", Try convert to: `{{type}}` |

#### Нет доступа к указанной диаграмме состояний

| Имя параметра | Значение |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | access_denied |
| __conveyor_set_param_return_description__ | Param: `{{param}}`, User: `{{user_id}}`, Conv_id: `{{diag_id}}` |

#### Указан ID процесса или диаграмма состояний удалена

| Имя параметра | Значение |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | access_refused |
| __conveyor_set_param_return_description__ | Param: `{{param}}`, Conv_id: `{{diag_id}}` is not state type |

> При использовании CONV в других логиках отличается только наименование параметров, значения те же.
