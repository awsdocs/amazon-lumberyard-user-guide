# Using GoalPipes to Trigger Communication<a name="ai-comm-goalpipes"></a>

To trigger a Communication event, use the goalop "communicate" as follows:

```
<GoalPipe name="Cover2_Communicate">
   <Communicate name="comm_welcome" channel="Search" expirity="0.5"/>
</GoalPipe>
```

Where,
+ **name** is the name of the actual communication \(sound or voice\)\. This is defined by the CommConfig property\. 
+ **channel** is the name of the Communication Channel this AI is Using\. The channel is defined in the Communication Channel file\.
+ **expirity** \(expiry\) is the maximum allowable delay in triggering the communication event when the Communication Channel is temporarily occupied\. If the communication event couldn't be triggered within this time period, it is discarded\.