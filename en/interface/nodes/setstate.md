# Set State logic

Addition of logic is possible only in the process with **[State diagram](../process_and_state/state_diagramm.md)** state

Allows to:
* Distribute incoming stream of data over the states
* Keep task states
* Accept state changes through task's "modify" using **[modify](logika_modify_task.md)** logic
* Process request to state diagram for getting data kept in Set State node 


Additional logic is available as part of SetState logic:
* [Condition](if.md) - allows to analyze incoming task parameters and distribute it to the required state
* [Alert when there is tasks queue](timer.md#tasks-limit) - allows to notify process while receiving critical amount of states (tasks) in the node 
* [Limit the time of the task in the node](timer.md#timer) - allows to transfer task to the next state by a a certain value of time


![Logic SetState](../img/process_and_state/setstate.gif)



