# Payment check/getting a voucher

Clone [folder "Payment check/getting a voucher”](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"

![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify:
*   `merchant` - merchant id
*   `payment_id` - unique payment identifier assigned by merchant

![](../img/status_skype.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:

*   `state` - payment status. `1` - successful; `0` - rejected;
*   `message` - extended message on payment status, it may contain a description of reasons because of which the payment is rejected
*   `voucherSerial` - Skype voucher serial number
*   `voucherCode` - code of Skype recharging

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - Error description
