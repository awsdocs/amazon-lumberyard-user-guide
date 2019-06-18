# Using AI Signals Among Agents<a name="ai-comm-signals"></a>

AI signals allow agents to communicate with each other\. An AI signal is sent by one AI agent to another AI agent, to a subset of agents, or to itself\. You can also specify how AI agents react to received signals\.

## Sending AI Signals<a name="ai-comm-signals-send"></a>

The method used to send an AI signal is as follows:

`AI:Signal(signalfilter_, signal_type, *MySignalName*, sender_entity_id);`

Where,

**signalfilter\_**  
Defines which AI agents receive the signal\. It can be chosen among a fixed set of symbols that have the prefix SIGNALFILTER\_\. The list of available signal filters is shown below\.

**signal\_type**  
Type of signal\.  
Values: `1` = The entity receiving the signal processes it only if it's enabled and it's not set to ignorant \(see AI:MakePuppetIgnorant for details\)\. \| `0` = The entity receiving the signal processes it if it's not set to Ignorant\. \| `-1` = The entity receiving the signal processes it unconditionally\.

**MySignalName**  
The signal identifier\. It can be any non\-empty string; for the signal recipient, it must be a function with the same name either in its current behavior, its default behavior, or in the DEFAULT\.lua script file in order to react to the received signal\.

**sender\_entity\_id**  
The entity id of the signal recipient\. This is usually the ID of the recipient, but can also be the entity ID of the sender if the signal will be sent to the sending agent\.


**Signalfilter Parameters**  

| Parameter | Description | 
| --- | --- | 
| 0 | The entity specified with the entity\_id parameter\. | 
| SIGNALFILTER\_LASTOP | The entity's last operation target \(if it has one\)\. | 
| SIGNALFILTER\_TARGET | The current entity's attention target\. | 
| SIGNALFILTER\_GROUPONLY | All the entities in the sender's group, i\.e\. the entities with its same group id, in the sender's communication range\. | 
| SIGNALFILTER\_SUPERGROUP | All the entities in the sender's group, i\.e\. the entities with its same group id, in the whole level\. | 
| SIGNALFILTER\_SPECIESONLY | All the entities of the same sender's species, in the sender's communication range\. | 
| SIGNALFILTER\_SUPERSPECIES | All the entities of the same sender's species, in the whole level\. | 
| SIGNALFILTER\_HALFOFGROUP | Half the entities of the sender's group \(you cannot specify which entities\)\. | 
| SIGNALFILTER\_NEARESTGROUP | The nearest entity to the sender in its group\. | 
| SIGNALFILTER\_NEARESTINCOMM | The nearest entity to the sender in its group, if in its communication range\. | 
| SIGNALFILTER\_ANYONEINCOMM | All of the entities in the sender's communication range\. | 
| SIGNALID\_READIBILITY | This special signal is used to make the entity recipient perform a readability event \(sound/animation\)\. | 

## Receiving AI Signals<a name="ai-comm-signals-receive"></a>

A signal that is received by an AI agent can cause an agent to change its behavior, as follows:

```
            Behavior1 = {
    OnEnemySeen   = *Behavior1*,
    OnEnemyMemory = *Behavior2*,
    MySignalName  = *MyNewBehavior*,
}
```

For example, if an AI agent is currently in Behavior1 and receives the signal `MySignalName`, after having executed the callback function above it will then switch its behavior to `MyNewBehavior`\.

The MySignalName function is defined as follows: 

`MySignalName = function(self, entity, sender)`

Where,

**self** is the AI agent behavior 

**entity** is the AI agent

**sender** is the signal sender

This function is actually a callback which, similar to system events, can be defined in the recipient entity's current behavior, the default idle behavior \(if it's not present in current behavior\), or in the Scripts/AI/Behaviors/Default\.lua script file \(if not present in the default idle behavior\)\.

Signal behaviors can be inherited, such as when a signal is used to initiate more than one behavior at a time\.