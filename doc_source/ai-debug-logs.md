# Using AILog and AISignals Files<a name="ai-debug-logs"></a>

The AILog\.log file can be used to log various AI agent events and the AISignals\.csv file can be used to store AI signals for debugging purposes\. 

**Note**  
These are only available if CryAISystem \(and CryAction in the case for AISignals\.csv\) were built in Debug Mode\.

The following AI events can be logged to the AILog\.log file:
+ AI Action started
+ AI Action ended
+ AI Action suspended
+ AI Action resumed
+ Signal received
+ Auxiliary Signal received
+ Goalpipe selected
+ Goalpipe inserted
+ Goalpipe reset
+ RefPoint position set
+ Stimulus registered
+ AI System reset
+ OnEnemyHeard
+ OnEnemyMemory
+ OnEnemySeen
+ OnInterestingSoundHeard
+ OnLostSightOfTarget
+ OnMemoryMoved
+ OnNoTarget
+ OnObjectSeen
+ OnSomethingSeen
+ OnSuspectedSeen
+ OnSuspectedSoundHeard
+ OnThreateningSeen
+ OnThreateningSoundHeard
+ AI Signal executing
+ Behavior constructor called
+ Behavior destructor called
+ Behavior selected