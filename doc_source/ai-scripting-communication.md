# Communication System<a name="ai-scripting-communication"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

AI communication is about playing sound/voice and/or animations at the right times in the course of the game\. 

Setting up communication for an AI agent requires the following steps:
+ General set up:
  + Define communication channels\. Channels are used to track the status of communication events for an AI\.
  + Define communications\. Communications detail specifically what activity should occur \(and how\) when the communication is called for\. Communications are grouped into configurations\.
  + Set up voice libraries\. Voice libraries support localized dialogs, subtitles, and lip\-syncing\.
+ Specify communication types for an AI using AI properties:
  + Point an AI's CommConfig property to a communication configuration, which contains the set of communications for that AI\.
  + Point an AI's esVoice property to a voice library to use for that AI\.
+ Trigger a communication event:
  + Specify the name of a communication channel for the event\.
  + Specify the name of a communication to fire\.

Communications, channels, and voice libraries are defined in a set of XML files\. At game start\-up, the directory `Game/Scripts/AI/Communication` and all subfolders are scanned for XML files containing these configurations\. 

## Defining Communication Channels<a name="ai-scripting-communication-channels"></a>

A communication channel determines whether an AI can play a communication at a given moment, depending on whether or not the communication channel is occupied\. Channels are a self\-contained concept, independent of other AI communication concepts\. They have a sole purpose: to be in one of two possible states, "occupied" or "free"\. 

AI communication channels are defined in an XML file stored in `Game/Scripts/AI/Communication`\. The SDK includes a template channel configuration XML file, called `ChannelConfg.xml`\. Communication channels are configured in a hierarchy of parent and child channels\. The hierarchical structure determines how a channel's occupied status affects the status of other channels \(for example, a parent of an occupied child channel\)\. 

### Channel Elements & Attributes<a name="ai-scripting-communication-channels-attributes"></a>

Communication channels are defined in a `<ChannelConfig>` element with the following attributes:

**name**  
Channel name\.

**priority**  
 

**minSilence**  
Minimum time \(in seconds\) that the channel should remain occupied after a communication has been completed\.

**flushSilence**  
Time \(in seconds\) that the channel should remain occupied after it has been flushed\. This value overrides the imposed silence time \(**minSilence**\) after playing a communication\. If not specified, the value set for **minSilence** is used\.

**actorMinSilence**  
Minimum time \(in seconds\) to restrict AI agents from playing voice libraries after starting a communication\.

**ignoreActorSilence**  
Flag indicating that AI agent communication restrictions from the script should be ignored\.

**type**  
Type of communication channel\. Valid values are "personal", "group" or "global"\.

### Example<a name="ai-scripting-communication-channels-example"></a>

```
Game/Scripts/AI/Communication/ChannelConfig.xml

<Communications>
    <ChannelConfig>
        <Channel name="Global" minSilence="1.5" flushSilence="0.5" type="global">
            <Channel name="Group" minSilence="1.5" flushSilence="0.5" type="group">
                <Channel name="Search" minSilence="6.5" type="group"/>
                <Channel name="Reaction" priority="2" minSilence="2" flushSilence="0.5" type="group"/>
                <Channel name="Threat" priority="4" minSilence="0.5" flushSilence="0.5" type="group"/>
            </Channel>
            <Channel name="Personal" priority="1" minSilence="2" actorMinSilence="3" type="personal"/>
        </Channel>
    </ChannelConfig>
</Communications>
```

## Configuring Communications for an AI<a name="ai-scripting-communication-configure"></a>

Communication configurations determine what communication activity AI agents can perform and how it will manifest\. Communications for a particular type of AI are grouped into configurations\. For example, your game might have both human and non\-human AI agents, each with its own set of communication activities\. In this scenario, you might group all the human communications into a configuration object named "human" while communications for non\-humans might be grouped into a "non\-human" configuration\. For a particular AI, you'll specify the configuration to use with the AI's *CommConfig* property\. With this configuration structure, you can define a communication \(such as "surprise"\) differently in each configuration so that, when triggered, the communication activity fits the AI involved\. 

For each communication, you also have the option to define multiple variations of action and specify how the variations are used\. 

AI communication channels are defined in one or more XML files stored in `Game/Scripts/AI/Communication`\. The SDK includes a template channel configuration XML file, called `BasicCommunications.xml`\. 

### Communication Elements & Attributes<a name="ai-scripting-communication-configure-attributes"></a>

Communications are configured using the following elements and attributes:

#### Config<a name="ai-scripting-communication-configure-configattributes"></a>

Communication configurations are grouped into `<Config>` elements and use the following attributes\. Each configuration must contain at least one communication\.

**name**  
Configuration name, which can be referenced in the AI's CommConfig property\. 

#### Communication<a name="ai-scripting-communication-configure-commattributes"></a>

A communication is defined in a `<Communication>` element with the following attributes\. Each communication should contain at least one variation\.

**name**  
Communication name\.

**choiceMethod**  
Method to use when choosing a variation\. Valid values include "Random", "Sequence", "RandomSequence" or "Match" \(uses only the first variation\)\.

**responseName**  
 

**responseChoiceMethod**  
Similar to **choiceMethod**\.

**forceAnimation**  
Boolean flag\.

#### Variation<a name="ai-scripting-communication-configure-varattributes"></a>

Each variation is defined in a `<Variation>` element with the following attributes\. 

**animationName**  
Animation graph input value\.

**soundName**  
 

**voiceName**  
 

**lookAtTarget**  
Boolean flag indicating whether or not the AI should look at the target during the communication\.

**finishMethod**  
Method that determines when communication is finished, such as after the communication type has finished or after a time interval\. Valid values include "animation", "sound", "voice", "timeout" or "all"\.

**blocking**  
AI behavior to disable during communication\. Valid values include "movement", "fire", "all", or "none"\.

**animationType**  
Valid values include "signal" or "action"\.

**timeout**  
 

### Example<a name="ai-scripting-communication-configure-example"></a>

```
Game/Scripts/AI/Communication/BasicCommunications.xml

<Communications>
<!--sound event example-->
    <Config name="Welcome">
        <Communication name="comm_welcome" finishMethod="sound" blocking="none">
            <Variation soundName="sounds/dialog:dialog:welcome" />
        </Communication>
    </Config>
<!--example showing combined animation + sound event (needs state using action/signal in the animation graph)-->
    <Config name="Surprise">
        <Communication name="comm_anim" finishMethod="animation" blocking="all" forceAnimation="1">
            <Variation animationName="Surprise" soundName="sounds/interface:player:heartbeat" />
        </Communication>
    </Config>
</Communications>
```

## Setting Up Voice Libraries<a name="ai-scripting-communication-voice"></a>

To support localized dialogs, subtitles, and lip syncing, you need to set up voice libraries\. Once set up, you can assign a voice library to an AI \(or entity archetype\) using the AI's *esVoice* property\.

Voice libraries are defined in a set of XML Excel files stored in `GameSDK/Libs/Communication/Voice`\. The SDK includes a template voice library file at `GameSDK/Libs/Communication/Voice/npc_01_example.xml`\. 

Each voice library must include the following information\.

**Language**  
Localization type for this library\.

**File Path**  
Location where the sound files for this library are stored\.

**Signal**  
Communication name associated with a sound file\.

**Sound File**  
File name of a sound file, listed by signal\.

**Example**  
Comment field used to describe or illustrate a sound file\.

### Example<a name="ai-scripting-communication-voice-example"></a>

**GameSDK/Libs/Communication/Voice/npc\_01\_example\.xml**


****  

|  |  | 
| --- |--- |
| Language | American English | 
| File Path | languages/dialog/ai\_npc\_01/ | 
| Signal | Sound File | SDK NPC 01 Example | 
| see | 
|  |  see\_player\_00  | i see you | 
|  |  see\_player\_01  | hey there you are | 
|  |  see\_player\_02  | hey i have been looking for you | 
| pain | 
|  | pain\_01 | ouch | 
|  | pain\_02 | ouch | 
|  | pain\_03 | ouch | 
| death | 
|  | death\_01 | arrrhh | 
|  | death\_02 | arrrhh | 
|  | death\_03 | arrrhh | 
| alerted | 
|  |  alerted\_00  | watch\_out | 
|  |  alerted\_01  | be careful | 
|  |  alerted\_02  | something there | 

## Setting Communication for an AI<a name="ai-scripting-communication-setting"></a>

An AI's communication methods are set using the AI agents properties\. You can set AI properties in several ways\. For information about using Lumberyard Editor to set AI properties, see [Using Database View to Set AI Communication](ai-comm-db.md)

Set the following properties:
+ *CommConfig* – Set this property to the name of the communication configuration you want this AI to use\. Communication configurations are defined in XML files in `Game/Scripts/AI/Communication`, using `<Config>` elements\. 
+ *esVoice* – Set this property to the name of the XML file containing the voice library you want this AI to use\. Voice libraries are defined in XML files in `GameSDK/Libs/Communication/Voice`\.

### Turning Animation and Voice Off<a name="ai-scripting-communication-turn-off"></a>

Communication animation and/or voice can be turned off for an AI agent using the agent's Lua script \(as in the example below\) or the entity properties in Lumberyard Editor Editor\.

#### Example<a name="ai-scripting-communication-turn-off-example"></a>

```
Game/Scripts/Entities/AI/Shared/BasicAITable.lua

Readability =
{
   bIgnoreAnimations = 0,
   bIgnoreVoice = 0,
},
```

## Triggering a Communication Event<a name="ai-scripting-communication-triggering"></a>

To trigger a communication event, use the goalop *communicate* with the following attributes\. Note that communication animations are not played if the AI is currently playing a smart object action\.

**name**  
Name of the communication to trigger \(sound, voice, and/or animation\)\. Communication names are defined in an XML file referred to by the CommConfig property of this AI\.

**channel**  
Communication channel being used by this AI\. An AI's communication channel is defined in an XML file in `Game/Scripts/AI/Communication`\.

**expirity \(expiry\)**  
Maximum allowable delay in triggering the communication when the communication channel is temporarily occupied\. If a communication can't be triggered within this time period, it is discarded\.

To trigger communications using flow graph logic, use the Flow Graph node **AI:Communication**\.

### Example<a name="ai-scripting-communication-triggering-example"></a>

```
<GoalPipe name="Cover2_Communicate">
   <Communicate name="comm_welcome" channel="Search" expirity="0.5"/>
</GoalPipe>
```

## Debugging<a name="ai-scripting-communication-debugging"></a>

To get debug information on AI communication issues, use the following console variables \(`ai_DebugDraw` should be set to "1"\):
+ ai\_DebugDrawCommunication
+ ai\_DebugDrawCommunicationHistoryDepth 
+ ai\_RecordCommunicationStats

Debug output is shown in the console as illustrated here:

```
Playing communication: comm_welcome[3007966447] as playID[84] 
CommunicationPlayer::PlayState: All finished! commID[-1287000849] 
CommunicationManager::OnCommunicationFinished: comm_welcome[3007966447] as playID[84] 
CommunicationPlayer removed finished: comm_welcome[3007966447] as playID[84] with listener[20788600]
```

## Troubleshooting<a name="ai-scripting-communication-troubleshooting"></a>

\[Warning\] Communicate\(77\) \[Friendly\.Norm\_Rifle1\] Communication failed to start

You may get this message or a similar one if your AI's behavior tree calls a communication but the communication configuration is not set up properly\. In this example message, "77" refers to line 77 in your AI's behavior tree script \(or goalop script\)\. This line is probably communication trigger such as this: 

```
<Communicate name="TargetSpottedWhileSearching" channel="Reaction" expirity="1.0" waitUntilFinished="0" />
```

Some things to check for::
+ Does the specified communication name "TargetSpottedWhileSearching" exist in your communication configuration files \(XML files located in `Game/Scripts/AI/Communication/`\)?
+ Check the *CommConfig* property for the AI\. Is it set to the name of a `<Config>` element defined in your communication configuration files? If so, is the communication name "TargetSpottedWhileSearching" defined inside this `<Config>` element? This issue, calling communications that aren't configured for the AI is a common source of this error\.
+ Check the communication's variation definition\. Does it point to a resource \(animation, sound\) that exists? If using a voice library, does it point to a valid voice library file name?