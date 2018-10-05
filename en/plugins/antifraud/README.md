# Transaction verification on antifraud

[Process template](https://www.corezoid.com/admin/edit_conv/15585) for transaction verification on antifraud is available in `"Examples - Antifraud"` folder.

In order to start working with process, clone the template following way.

![](../img/mandrill_copy_conveyor.png)

Go to `dashboard` mode and press `Add task` button - add task.

![](../img/mandrill_dashboard.png)

In appeared window, specify all required parameters.

After all task parameters are specified , press `Send task` button.

Result of work process will be the task moving through process and going to the one of end states (red color node).

**In case of success returns:**
* `action` - result of transaction verification on antifraud
* `description` - description

`action` possible values:
* `true` -  you can make an operation 
* `decline` - transaction declined
* `manual` - transfer for manual processing (delay)
* `merchant_check` - you can make an operation but there's a need to double-check the activities of the merchant.
* `merchant_block` - decline of making operation and changing the merchant status to "blocked"

**In case of error**, task will go to the escalation node and next parameters will be added:
* `errorCode` - 0001
* `__conveyor_rpc_reply_return_description__` - Error calling API. Repeat the request again if it necessary

