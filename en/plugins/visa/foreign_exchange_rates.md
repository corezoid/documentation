# Currency rates

[Template](https://admin.corezoid.com/editor/55510/89545) process of getting VISA's currency rates.

[Description of API Foreign ExchangeRates](https://developer.visa.com/products/foreign_exchange) on the VISA website.


Select the **"Set parameter"** logic and fill the fields **userID** and **password** with [username and password](https://doc.corezoid.com/en/plugins/visa/access.html) values from the VISA administrator panel
![](../img/visa/set_password.png)

The next step is to select the API logic and expand the "Additionally" block,
![](../img/visa/api_add.png)

You have to insert the [private key](https://doc.corezoid.com/en/plugins/visa/access.html) and [test certificate](https://doc.corezoid.com/en/plugins/visa/access.html) provided to you by VISA to the "Sign the request by certificate" module.
![](../img/visa/api_cert.png)

The key and certificate should be inserted in the following order:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
```

After this you may go to **VIEW** mode and send a test request by pressing the button **"Add task"**:

![](../img/visa/test_api.png)

It should contain the following parameters:
*   `sourceCurrencyCode` - [currency code](https://developer.visa.com/request_response_codes#isoCodes) of initial amount
*   `destinationCurrencyCode` - [currency code](https://developer.visa.com/request_response_codes#isoCodes) which we want to convert the amount to
*   `sourceAmount` - amount

Once the parameters are filled, press **"Send task"**.

Result of API operation:
*   `destinationAmount` -  total amount after conversion
*   `conversionRate` - conversion rate

> The template contains the [URL](https://sandbox.api.visa.com/forexrates/v1/foreignexchangerates) of the sandbox. To get access to the operational environment it is necessary to refer to [developer@visa.com](mail:developer@visa.com)
