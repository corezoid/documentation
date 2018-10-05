# Getting available Skype vouchers

To get available Skype vouchers, [register the merchant](https://api.privatbank.ua/api-privat24/p24registration.md) in Privat24 system.

**Privat24 Merchant** is an additional account of Privat24 which allows to make online payments in the automatic mode.

As a result of registration, you’ll get `merchant id` and `merchant password`, which allow to integrate payment and information services of Privat24 to you web-site.

Clone [folder "Getting available Skype vouchers"](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"

![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify:
*   `merchant` - merchant id

![](../img/nominals.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:

* `nominals`- available Skype vouchers

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - Error description
