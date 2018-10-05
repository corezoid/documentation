# P2P платежи с карты на карту

Используя набор API VISA и MasterCard, мы постороили [готовые процессы](https://admin.corezoid.com/folder/conv/103469).

Общая схема P2P выглядит следующим образом:
![](../img/visa/p2p_schema.png)

Эту схему реализует [процесс-ядро "Core"](https://admin.corezoid.com/editor/103468/158929).

## Подготовка

**1)** Добавьте Ваши ключи и все остальные необходимые параметры в узел "Config" процесса ["MAIN"](https://admin.corezoid.com/editor/103469/158898)- замените переменные в двойных фигурных скобках ({{visa_user}}, {{visa_password}} и т.д.) на постоянные значения.

![](../img/visa/config.png)

>Именно этот процесс и есть начало реализации P2P.

**2)** Добавьте RSA Private key и CERTIFICATE Visa во все узлы процессов, где есть вызов API Visa.

Для этого подсветите узел, нажмите  `Additionally`

![](../img/visa/sertificate.png)

В поле `Sign the request by certificate` вставьте RSA Private key и CERTIFICATE Visa в пустые строки между

`-----BEGIN RSA PRIVATE KEY-----`

`-----END RSA PRIVATE KEY-----`

и

`-----BEGIN CERTIFICATE-----`

`-----END CERTIFICATE-----`

соответсвенно.

![](../img/visa/sertificate_1.png)

Все процессы, где есть вызов API Visa расположены в [папке "VISA"](https://admin.corezoid.com/folder/conv/103463).

Путь к папке: [Examples](https://admin.corezoid.com/folder/conv/1833) -> [P2P VISA & MC](https://admin.corezoid.com/folder/conv/103469) -> [Core](https://admin.corezoid.com/folder/conv/103468) -> [APIs](https://admin.corezoid.com/folder/conv/103465) -> [VISA](https://admin.corezoid.com/folder/conv/103463)


## Тестовые данные для Visa

```json
{
    "address" : {
        "county": "San Mateo",
        "state": "CA",
        "zipCode": "94404",
        "country": "USA",
        "city" : "Dnepr"
        },
    "card":"4895142232120006",
    "card_cvv":"111",
    "card_date":"2017-11",
    "receiver_card":"4895142232120006",
    "amount":1,
    "currency":"USD",
    "fee":0,
    "sender_name":"Dima",
    "receiver_name":"Dima 2",
    "order_id":123
}
```

Для тестирования возврата необходимо указать:

receiver_card = 4895142232120005

## Дополнение

Для реализации полноценной схемы Р2Р переводов MasterCard необходима доработка такого функционала как:
* Watch List Screening
* Account Validation

В текущей версии процессов эти этапы просто игнорируются (Логика GO).

Для обеих схем Р2Р (Visa и MasterCard) на этапе предподготовки ("Prepare" - первый узел процесса ["Core"](https://admin.corezoid.com/editor/103468/158929)) стоит "заглушка" - параметры, которые планируется получить устанавливаются с помощью Логики CODE.

Реализация указанного функционала в работе. Будет добавлен с новой версией процессов.
