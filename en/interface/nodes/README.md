# Nodes and logic


>Demonstrating and [basic knowledge](https://new.corezoid.com/tutorials/basic-tutorial/) in [TUTORIALS](https://new.corezoid.com/tutorials/) section on [site](https://new.corezoid.com)

Every Corezoid process is made of nodes.

Every node contains its uniqe logic.

Tasks move through the procces from node to node, following specified logic.

![](../img/create/nodes.png)

| Logic name | Description|
| -- | -- |
|Delay| Time interval (delay), at which task will go further through process, also specified critical amount of tasks in node - task limit|
|Condition| Going by the condition. Possible conditions =, !=, <, >, regex|
|API Call| External API call with parameters|
|Waiting for Callback| Waiting for reply by request from external system|
|Code| Possibility to realize an additional task processing logic with one of the languages (JavaScript, Erlang) |
|Copy task| Copy task in a different process|
|Modify task| Updating task in a different process|
|Call Process| Call unique process|
|Reply to Process| Reply to universal process call|
|Sum| Sum of the amount by a certain tas filed|
|Set Parameter| Set the parameter / modifying parameters value in the task|
|Set State| Implementation of storage logic и and task state distribution|
|Queue| Implementation of queue logic|
|Get from Queue| Received tasks from the queue|
|End: Success| End node that contains successful process tasks
|End: Error| End node that contains tasks with process errors|


