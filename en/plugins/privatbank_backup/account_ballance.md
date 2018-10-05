# Current balance on merchant account

To get the balance on merchant account, [register the merchant](https://api.privatbank.ua/api-privat24/p24registration.md) in Privat24 system.

**Privat24 Merchant** is an additional account of Privat24 which allows to make online payments in the automatic mode.

As a result of registration, you’ll get `merchant id` and `merchant password`, which allow to integrate payment and information services of Privat24 to you web-site.

Clone [folder "Current balance on merchant account"](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.


![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"
![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request 
![](../img/mandrill_dashboard.png)

In the opened form specify parameters of the request and click on "Send task".

* `merchant` - merchant id
* `card` - card number
* `payment_id` - unique payment identifier assigned by merchant
* `country` - merchant country

![](../img/account_ballance.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:
* `Currency`  - Currency
* `Date` - Date and time of balance updating
* `Fin_Limit`  - Credit limit
* `Card` - Card number
* `Type`  - Account type
* `Balance` - Balance

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - Error description