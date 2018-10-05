# Creation of payment for Skype voucher

To create a payment, [register the merchant](https://api.privatbank.ua/api-privat24/p24registration.md) in Privat24 system.

**Privat24 Merchant** is an additional account of Privat24 which allows to make online payments in the automatic mode.

As a result of registration, you’ll get `merchant id` and `merchant password`, which allow to integrate payment and information services of Privat24 to you web-site.

Clone [folder "Creation of payment for Skype voucher"](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"

![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify:
*   `merchant` - merchant id
*   `payment_id` - unique payment identifier assigned by merchant
*   `nominal` - nominals of skype vouchers (USD)

![](../img/skype_buy.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:

* `currency`- currency of operation
* `state` - payment status.`1` - successful; `0` - rejected;
* `message`- extended message on payment status, it may contain a description of reasons because of which the payment is rejected
* `ref`- internal reference of payment in Privat24 assigned in the banking system. Payment identifier in Privat24. (In case the payment is rejected, the field is left blank)
* `amount`- payment amount

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - error description
