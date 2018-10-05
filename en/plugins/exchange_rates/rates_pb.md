# PrivatBank exchange rates

Clone [process template](https://www.corezoid.com/admin/edit_conv/27937) to get PrivatBank exchange rates

![](../img/mandrill_copy_conveyor.png)

Go to `dashboard`, click `Add task` (to add the request) and `Send task` (to send the request).

![](../img/mandrill_dashboard.png)

**In case of success** the following parameters are added to the request:

* `buy_USD`- US dollar buying rate
* `buy_EUR`- Euro buying rate
* `buy_RUR`- Russian ruble buying rate
* `sale_USD`- US dollar selling rate
* `sale_EUR`- Euro selling rate
* `sale_RUR`- Russian ruble selling rate

**In case of error** the request is transferred to the escalation node with the parameter:
* `Error` - Error description
