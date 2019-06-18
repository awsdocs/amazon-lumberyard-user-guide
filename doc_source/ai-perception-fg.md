# Using Flow Graph to Set Agent Perception<a name="ai-perception-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can use the following AI flow graph nodes to affect agent perception\. The perception scaling nodes are important as they control the degree to which AI agents can see or hear their surroundings\.
+ **AI:AIAwarenessToPlayer** – The degree to which an AI agent is aware of the player's faction\. Red is the most aware, while green is the least aware\.
+ **AI:AIGlobalPerceptionScaling** – The degree of perception \(as a percentage\) for all AI agents or factions in a level\.
+ **AI:PerceptionScale** – The degree of perception \(as a percentage\) for a single AI agent\.
+ **AI:AlertnessState** – The degree to which any faction or AI agent type is aware of other factions or agent types\.
+ **AI:GroupAlertness** – Similar to AI:AlertnessState, but by group ID\.
+ **AI:AttentionTarget** – Gets the target of an AI agent's attention as a position or entityID\.

**To access Flow Graph perception nodes**

1. Open Flow Graph\.

1. In the **Flow Graphs** pane, select your asset\.

1. Right\-click anywhere in the graph, then click **Add Node, AI** \(or **Input**\) to access the nodes\.

You can use additional flow graph logic to fine\-tune AI agent control and determine how agent awareness varies with the agent's surroundings, as shown below\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/ai-perception-fg.png)