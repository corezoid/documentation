## Getting value of task parameters

With CONV you could get whole task from diagram:

`{{conv[{{diag_id}}].ref[{{ref}}]}}`

or the parameter value from task:

`{{conv[{{diag_id}}].ref[{{ref}}].param}}`

From process or final node data couldn't be read.

Example:

    //returns whole task with REF = menu from diagram with ID = 123456 (you need to specify parameter type Object)

    {{conv[123456].ref[menu]}}

    // returns parameter value amount from task with REF = qwerty diagram with ID = 123456

    {{conv[123456].ref[qwerty].amount}}

    // returns value from task with REF = {{ref}} and diagramm with ID = {{diag_id}}

    {{conv[{{diag_id}}].ref[{{ref}}].ID_параметра}}

With using CONV follow **checks** are performed:
* specified ID of the state diagram, not the process
* state diagram is not deleted
* there is access to the specified state diagram

### Error types

Here describes the errors that occur when using CONV in the Set Parameter logic.

#### Invalid parameter type or parameter in the specified task is missing

| Parameter name  | Value |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | set_param_wrong_convert_param |
| __conveyor_set_param_return_description__ | Param: {{param}}, Value: {{value}}", Try convert to: {{type}} |

#### There is no access to the specified state diagram

| Parameter name  | Value |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | access_denied |
| __conveyor_set_param_return_description__ | Param: {{param}}, User: {{user_id}}, Conv_id: {{diag_id}} |

#### Specified process ID or state diagram deleted

| Parameter name | Value |
| --- | --- |
| __conveyor_set_param_return_type_error__ | software |
| __conveyor_set_param_return_type_tag__ | access_refused |
| __conveyor_set_param_return_description__ | Param: {{param}}, Conv_id: {{diag_id}} is not state type |

> When using CONV in other logics, only the name of the parameters is different, the values are the same.