# p2p


The example of  p2p process - [process  11719](https://www.corezoid.com/admin/edit_conv/11719)

It is available in your folder `"Examples - LiqPay - p2p"`.

In order to start working with it, clone the example as follows:
![](../img/mandrill_copy_conveyor.png)

Insert your `private key` from LiqPay in the field `Secret key`:
![](../img/LiqPay_insert_key.png)

Generate a callback URL for retrieving the payment results from LiqPay
![](../img/LiqPay_callback_url.png)

by clicking on "Create callback URL"
![](../img/LiqPay_callback_url_generate.png)

You get a URL, then you need to specify a value `obj_id` in the field `Path to task_id`
![](../img/LiqPay_callback_url_copy.png)

Then copy the URL and paste it into the field `callback` of logic API, which is in a node `Call API LiqPay`.
![](../img/LiqPay_callback_url_insert.png)

Switch to the `dashboard` mode and click on `Add task` - for sending a test request.

![](../img/mandrill_dashboard.png)

Indicate your payment parameters in the opened form and click on "Send task".

The process is prepared for the use from other processes through logic RPC. The list of output parameters:
*   If  error
    *   `err_description` - error description
    *   `err_code` - error code
*   If successful
    *   `result` - contains the value `success`
