# State diagram

The state diagram is commonly used to track the objects' states and store the operational data.

> For example, user states:
- new
- active
- non-active


There is a limited set of nodes available in the state diagrams:

| Node type | Description|
| -- | -- |
|Delay| Is used to delay the task in the node for the specified time. Time interval (delay) is specified the field Limit the time of the task in the node. |
|Condition| It is responsible for conditional logic operators “if …, then …”. |
|Set state| Allows you to track objects' states and store an operational data. |
|Code| If you feel a lack of the available logic types, you can use Code node to write a custom code than will be applied to the task.|
|Copy task| Allows us to copy a task from one process to another while the original process is still running and without interrupting it. |
|Modify task| Allows you to modify a task in another process by reference. |
|Set Parameter| allows you to add new and modify existing parameters in tasks. It also allows you to apply various functions to the parameters. |
| Queue | Allows you to store data in the node. |



