# Курсы валют

####[Шаблон процесса](https://admin.corezoid.com/editor/55510/89545) получения курсов валют VISA.

[Описание API Foreign ExchangeRates](https://developer.visa.com/products/foreign_exchange) на сайте VISA.


Выберите логику **"Set parameter"** и заполните поля **userID** и **password** значениями [логина и пароля](https://doc.corezoid.com/ru/plugins/visa/access.html) из админ. панели VISA
![](../img/visa/set_password.png)

Следующим этапом необходимо выбрать логику API, развернуть блок "Additionally",
![](../img/visa/api_add.png)

В котором необходимо в блок "Sign the request by certificate" вставить выданные Вам VISA [приватный ключ](https://doc.corezoid.com/ru/plugins/visa/access.html) и [тестовый сертификат](https://doc.corezoid.com/ru/plugins/visa/access.html).

![](../img/visa/api_cert.png)

Вставлять ключ и сертификат необходимо в следующем порядке:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
```

После этого можно перейти в режим **VIEW** и отправить тестовую заявку нажав кнопку **"Add task"**:
![](../img/visa/test_api.png)

Со следующими параметрами:
*   `sourceCurrencyCode` - [код валюты](https://developer.visa.com/request_response_codes#isoCodes) исходной суммы
*   `destinationCurrencyCode` - [код валюты](https://developer.visa.com/request_response_codes#isoCodes) в которую мы хотим конвертировать сумму
*   `sourceAmount` - сумма

После того как параметры заполнены нажмите **"Send task"**.

Результат работы API:
*   `destinationAmount` - итоговая сумма после конвертации
*   `conversionRate` - по какому курсу произошла конвертация

> В шаблоне указан [URL](https://sandbox.api.visa.com/forexrates/v1/foreignexchangerates) песочницы (sandbox). Для получения доступа к боевой среде необходимо обращаться на [developer@visa.com](mail:developer@visa.com)


