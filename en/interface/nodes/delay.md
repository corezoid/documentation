# Delay logic

Used to delay the task in the node for the specified time.

![semafor_timer](../img/create/delay.png)

Time interval (delay) is specified the field **Limit the time of the task in the node**.

After the time expires, the task goes to the specified node.

This value can be specified with:

* exact number and unit of measurement - seconds (min 30), minutes, hours, days.

![](../img/create/delay_const.png)

* task parameter:

![](../img/create/delay_param.png)

This task parameter must contain date/time in **unixtime** format.
At the specified time the task goes to a specified node.

![](../img/create/unix_param.png)

* function `$.unixtime()` to get the Unix timestamp of the exact time

![](../img/create/delay_func.png)

If the process is highly loaded, value **60 seconds** for **Delay** logic is recommended

## Example of a dynamic timer for each task

See [an example](https://admin.corezoid.com/editor/102672/156747), where:
*   variable `date` is converted to **unixtime** fo specifying in **Delay** logic (the format is `DD.MM.YYYY hh:mm:ss`)
*   variable `offset_GMT` is used to correct value to Corezoid server time zone.

