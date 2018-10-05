# P2P payments from card to card

Using VISA and MasterCard API kit, we have built [prepared processes](https://admin.corezoid.com/folder/conv/103469).

The common P2P scheme looks in following way:
![](../img/visa/p2p_schema.png)

This scheme is realized by [core-process "Core"](https://admin.corezoid.com/editor/103468/158929).

## Prerparing

**1)** Add your keys and all other required parameters in "Config" node of ["MAIN"] process (https://admin.corezoid.com/editor/103469/158898)- replace variables in double braces ({{visa_user}}, {{visa_password}} etc.) by constant values.

![](../img/visa/config.png)

>Exactly this process is the beginning of P2P realization.

**2)** Add RSA Private key and CERTIFICATE Visa to all Visa process nodes where Visa API run is.

For this, highlight node, press `Additionally`

![](../img/visa/sertificate.png)

Paste RSA Private key in `Sign the request by certificate` field and CERTIFICATE Visa in empty lines between

`-----BEGIN RSA PRIVATE KEY-----`

`-----END RSA PRIVATE KEY-----`

and

`-----BEGIN CERTIFICATE-----`

`-----END CERTIFICATE-----`

respectively.

![](../img/visa/sertificate_1.png)

All processes, where Visa API running is, are located in ["VISA" folder](https://admin.corezoid.com/folder/conv/103463).

Path to the folder: [Examples](https://admin.corezoid.com/folder/conv/1833) -> [P2P VISA & MC](https://admin.corezoid.com/folder/conv/103469) -> [Core](https://admin.corezoid.com/folder/conv/103468) -> [APIs](https://admin.corezoid.com/folder/conv/103465) -> [VISA](https://admin.corezoid.com/folder/conv/103463)


## Test data for Visa

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

For refund test you need to specify:

receiver_card = 4895142232120005

## Additional

For full P2P MasterCard transaction scheme realization there has to be rework of such functional as:
* Watch List Screening
* Account Validation

In the current version of processes these steps are just ignored. (GO logic).

For both P2P scheme (Visa and MasterCard) on pretreatment step ("Prepare" - First process node ["Core"](https://admin.corezoid.com/editor/103468/158929)) there's "gag" - the parameters planned to get are setting up with CODE Logics
Specified functional realization is in work. It would be updated with new version of processes.
