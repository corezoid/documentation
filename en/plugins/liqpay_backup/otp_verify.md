# Transaction confirmation using OTP password

Clone [folder "Transaction confirmation using OTP password"](https://admin.corezoid.com/folder/conv/1923) to get the process and dashboard.

![](../img/copy_folder.png)

Go to the process.

In the process **generate a link to get callback from LiqPay** - in the node with the Logic Callback `"Receive Callback"` click on the icon "Corezoid" and the link will be copied into the clipboard.
In the field `Path to task_id` specify `obj_id`.

![](../img/corezoid_callback.png)

Obtained URL should be inserted in the value of `callback` parameter of API logic, located in the node `Calling API`.

![](../img/liqpay_callback.png)

Insert your `private key` from LiqPay in the node `Calling API` in the field `Secret key`:
![](../img/api_secret_outer.png)

For testing the process, go to the mode `dashboard` and click `Add task` - to add the request.

![](../img/mandrill_dashboard.png)

In the opened form specify the required parameters and click on "Send task":

* `public_key` - Public key of the shop
* `token` - token received in response to initialization request
* `otp` - OTP (one-time password) received by the Customer on his/her phone number after initialization request

![](../img/otp.png)

Then press the button `Send task` - to send the request.

**In case of successful transaction for cards without 3-D Secure** the following parameters are added to the request:
* **status** - payment status
 * `success` - successful payment
* **payment_id** - payment id number in LiqPay

** In case of successful creation of the shop in LiqPay system** the following parameters are added to the request:
* **public_key**  - public key –shop identifier
* **private_key**  - private key – shop access key

**In case of error** the request goes to the escalation node with the parameter below:
* **err_code** - Error code
* **err_description** - Error description
