## Time logic
![semafor_timer](../img/create/semafor_timer.png)

Work logic:

 - `Value logic` is a boundary value in seconds, reaching which a request is automatically moved to escalation node. Possible options: in seconds, iminutes, hours, days {% raw %}{{varibale from the request}}{% endraw %} date/time in the format unixtime
 - `Select to go node` and `Select escalation node` are the same at this moment as they specify the node for passing when executing escalation conditions (`Value logic`)

![semafor_timer_example](../img/create/semafor_timer_example.png)
