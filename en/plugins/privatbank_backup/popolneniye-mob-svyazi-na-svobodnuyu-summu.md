# Recharging mobile communication account with free amount

To recharge mobile communication account with free amount, [register the merchant](https://api.privatbank.ua/api-privat24/p24registration.md) in Privat24 system.

**Privat24 Merchant** is an additional account of Privat24 which allows to make online payments in the automatic mode.

As a result of registration, you’ll get `merchant id` and `merchant password`, which allow to integrate payment and information services of Privat24 to you web-site.

Clone [folder "Recharging mobile communication account with free amount"](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"

![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify:
*   `amount` - payment amount
*   `operator` - service (operator). Beeline Ukraine - `RPBLUA`, Kyivstar - `RPKSTR`, Life :) - `RPLIFE`, МТС Ukraine - `RPMTSU`, PEOPLEnet - `PPNET`, Utel - `RPUTEL`, Internet Kyivstar - `RPKSIN`
*   `phone` - phone number
*   `merchant` - merchant id
*   `payment_id` - unique payment identifier assigned by merchant. It is repeated in response to the request, stored in Privat24 database, and serves for unambiguous comparison of operations on payment partner side with operations in Privat24.

![](../img/mob_ref.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:
* `state`- payment state (1 - successful, 0- rejected)
* `ref` - internal reference of payment in Privat24 assigned in the banking system. Payment identifier in Privat24. (In case the payment is rejected, the field is left blank)
* `message` - extended message on payment status, it may contain a description of reasons because of which the payment is rejected
* `commission` - bank commission amount
* `currency` - currency of operation

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - Error description
