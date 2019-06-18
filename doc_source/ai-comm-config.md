# Using the CommConfig Property<a name="ai-comm-config"></a>

The `CommConfig` property \(see [Using Database View to Set AI Communication](ai-comm-db.md)\) determines which communications \(and how\) an AI agent can play\. This property has a value of **Basic** or **Human**, whose properties and attributed are defined by two XML files\.

A sample `BasicCommunications.xml` file is shown below:

```
<Communications>
   <!--Animation + Sound Event example (needs state using the action/signal in the animation graph)-->
  <Config name="Surprise">
    <Communication name="comm_anim" finishMethod="animation" blocking="all" forceAnimation="1">
        <Variation animationName="Surprise" soundName="sounds/interface:player:heartbeat" />
    </Communication>
  </Config>
 
  <!--Sound Event example-->
  <Config name="Welcome">
    <Communication name="comm_welcome" finishMethod="sound" blocking="none">
      <Variation soundName="sounds/dialog:dialog:welcome" />
    </Communication>
  </Config>
 
  <!--Auto generated Voice Library examples-->
  <Config name="SDK_Example_NPC_01">
    <AutoGenerateCommunication voiceLib="npc_01_example" finishMethod="voice" blocking="none" />
  </Config>
 
  <Config name="SDK_Example_NPC_02">
    <AutoGenerateCommunication voiceLib="npc_02_example" finishMethod="voice" blocking="none" />
  </Config>
</Communications>
```

Where,
+ **name**: Basic or Human, as specified by the CommConfig property\.
+ **choiceMethod**: Method used to choose a variation: Random, Sequence, RandomSequence, or Match\.
+ **responseChoiceMethod**: Method used to choose a variation: Random, Sequence, RandomSequence, or Match\.
+ **animationName**: Animation graph input value
+ **lookAtTarget: **: Valid values are 1\|0, true\|false, or yes\|no\. Makes the AI look at the target\.
+ **finishMethod**: Any or all of: animation, sound, voice, timeout, all\. It defines the way to determine when the communication is finished \- after the animation is finished, or time interval has elapsed\.
+ **blocking**: movement, fire, all, none\. It allows to disable the movement or firing of the AI\.
+ **animationType**: signal or action
+ **voiceLib**: The name of the Voice Library to extract Communication names from\.