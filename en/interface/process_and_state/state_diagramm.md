# State diagram

Uses for object state accounting.

> For example, stets of users:
- new
- active
- non-active

State diagram gives such opportunities:
-   object state accounting
-   object in node data keeping
-   receiving object data using [CONV](../functions/getParamFromApp.md) function
-   no limits for amount of tasks in process

In state diagram there is a limited logic set available:

| Name of logic | Description|
| -- | -- |
|Delay| Time interval (delay) at which the task will go further thorugh process, is indicated and critical amount of tasks in the node -  task limit|
|Condition| Transition on the condition. Variants of conditions =, !=, <, >, regex|
|Set state| Set state and waiting for its changes|
|Code| Possibility to realize additional task processing logic in one of the languages (JavaScript, Erlang) |
|Copy task| Copy task in a different process|
|Modify task| Updating task in a different process|
|Set Parameter| Set the parameter / change parameter's value in the task|
|Queue| Realizing queue logic|



