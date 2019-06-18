# Using the AI Debug Recorder<a name="ai-debug-recorder"></a>

The AI Debug Recorder is a recording tool that logs all inputs, decisions, computations and other useful data for an AI agent in real\-time while the game is being played\. At the end of the game session, the recorder serializes all the data for future processing\. 

There are several ways to start or stop an AI debug recording session, as follows:
+ **Automatically using the Console** – Use the `ai_Recorder_Auto` console variable to automatically begin recording whenever a new game session starts\. Similarly, the recording stops and saves when the game session ends, by whatever means \(except the game crashing\)\. 
+ **Manually using the Console** – Use the `ai_Recorder_Start` and `ai_Recorder_Stop` console variables to start or stop a recording as needed\.
+ **Manually in Code** – Use the `IAIRecorder` interface to start or stop a recording as needed\.

## Recorder Output File<a name="ai-debug-recorder-output"></a>

Regardless of which method is used to perform a recording, all recordings are saved within the `\Recordings` folder in the Lumberyard root directory \(`lumberyard_version\dev`\)\. The file name of the recording is formatted as follows:

*MapName\_Build\(A\) Date\(B\) Time\(C\)\.rcd*
+ *MapName * – The name of the map in which the recording took place\. The exception is if the recording took place in Lumberyard Editor, in which case the map name is EDITORAUTO as a suffix\.
+ *Build\(A\) * – Version of the build with which the recording was made\. We recommended using the same build version to view the recording\.
+ *Date\(B\) * – Date the recording was made\.
+ *Time\(C\) * – The time the recording was saved\.

**Note**  
If you create a manual recording, you enter your own file name to use\. If none is specified, the above format is used\.

## Recorder Data Streams<a name="ai-debug-recorder-newdata"></a>

An AI Debug recording consists of many data streams that chronologically log a specific type of input, as follows\. It is also possible to add a new stream to the recording if needed\.
+ E\_RESET – When the agent is reset\.
+ E\_SIGNALRECIEVED – When the agent receives a signal\.
+ E\_SIGNALRECIEVEDAUX – When the agent receives an auxiliary signal\.
+ E\_SIGNALEXECUTING – When the agent is executing a received signal \(processing it\)\.
+ E\_GOALPIPESELECTED – When the agent selects a new goal pipe\.
+ E\_GOALPIPEINSERTED – When the agent inserts a new goal pipe\.
+ E\_GOALPIPERESETED – When the goal pipe on the agent is reset\.
+ E\_BEHAVIORSELECTED – When the agent selects a new behavior\.
+ E\_BEHAVIORDESTRUCTOR – When the agent's current behavior has its destructor called\.
+ E\_BEHAVIORCONSTRUCTOR – When the agent's current behavior has its constructor called\.
+ E\_ATTENTIONTARGET – When the agent's attention target changes\.
+ E\_ATTENTIONTARGETPOS – When the position of the agent's attention target changes\.
+ E\_REGISTERSTIMULUS – When the agent receives a perception stimulus\.
+ E\_HANDLERNEVENT – When the agent's mind handles an event\.
+ E\_REFPOINTPOS – When the agent's reference point position changes\.
+ E\_AGENTPOS – When the agent's position changes\.
+ E\_AGENTDIR – When the agent's look direction changes\.
+ E\_LUACOMMENT – When a Lua comment is made on the agent\.
+ E\_HEALTH – When the agent's health changes\.
+ E\_HIT\_DAMAGE – When the agent receives hit damage\.
+ E\_DEATH – When the agent is killed\.
+ E\_SIGNALEXECUTEDWARNING – When the agent is taking too long to process a signal\.
+ E\_BOOKMARK – When a bookmark is placed on the agent\.

To record information for any of these events, use the `IAIRecordable` interface \(which all AI Objects inherit from, and is used to link to the AI Debug Recorder itself\)\. 

All of the data streams listed are handled by the AI System with the exception of the Bookmark stream\. This is a special stream that is used to mark areas of interest for easy debugging later\.

For example, a game project may connect a keyboard input to log event data on the Bookmark stream whenever a button is pressed, which informs the QA team to push the button whenever odd behavior from the AI is observed\.