# GET TASK logic

**GET TASK logic** allows getting tasks from the process and node to which API queue Logic is added.

![API_get_task](../interface//img/create/API_get_task.png)

* **Process** - select the process from the drop-down list by the process id or its name (only the processes available to the user may be selected).
* **Node** - from the drop-down list or by name it is necessary to select the node of the above-mentioned process and to which API queue Logic is being added.
* **Order_by** may have the following parameters:
    *   **ASC** - get the first task (the oldest one by time) from the queue
    *   **DESC** - get the latest task (the latest one by time) from the queue

Dynamic values of the tasks parameters may be used in **Process** and **Node**. For example: {{conv_id}} - process id, {{node_id}} - node id.

**If successful**, the current task will be added with
* `__queue_task_id__` - ID of the task from node queue
* `__queue_task_data__` - json object of the task parameters from the node with API queue Logic


####Error type


**No tasks in the node with QUEUE Logic**

| Parameter name | Value |
| -- | -- |
| `__conveyor_get_task_return_type_error__` | software |
| `__conveyor_get_task_return_type_tag__` | get_task_executing_error |
| `__conveyor_get_task_return_description__` | not_found_task |

**User has no access to the process with QUEUE Logic**

| Parameter name | Value |
| -- | -- |
| `__conveyor_get_task_return_type_error__` | software |
| `__conveyor_get_task_return_type_tag__` | get_task_executing_error |
| `__conveyor_get_task_return_description__` | access_denied |

**The process or node specified has no QUEUE Logic**

| Parameter name | Value |
| -- | -- |
| `__conveyor_queue_return_type_error__` | software |
| `__conveyor_queue_return_type_tag__` | queue_wrong_logic |
| `__conveyor_queue_return_description__` | No queue logic in conv_id:  |

**Incorrect transmission of process id or node id upon dynamic use**

| Parameter name | Value |
| -- | -- |
| `__conveyor_get_task_return_type_error__` | software|
| `__conveyor_get_task_return_type_tag__` | get_task_wrong_convert_param|

**Kernel error**

| Parameter name | Value |
| -- | -- |
| `__conveyor_get_task_return_type_error__` | hardware |
| `__conveyor_get_task_return_type_tag__` | get_task_fatal_error |
| `__conveyor_get_task_return_description__` | Error running get task |
