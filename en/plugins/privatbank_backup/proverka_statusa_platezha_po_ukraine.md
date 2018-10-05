# Checking status of payment in Ukraine

Clone [folder "Checking status of payment in Ukraine"](https://admin.corezoid.com/folder/conv/6081) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the node "Calling API" add merchant password in the field "Secret key"

![](../img/secret.png)

For testing the process, go to the mode `dashboard` and click `Add task` to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify:
*   `ref` - internal reference of payment in Privat24
*   `merchant` - merchant id
*   `payment_id` - unique payment identifier assigned by merchant

![](../img/check.png)

Then press the button `Send task` - to send the request.

**In case of success** the following parameters are added to the request:
* **state** - payment status:

`not found` - payment cannot be found; `ok` - successful; `err` - rejected; `snd` - in progress


* **message** - extended message on payment status, it can be

**In case of error** the request goes to the escalation node with the parameter below:
* `Error` - Error description
