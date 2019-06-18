# Using Flow Graph to Spawn AI Agents<a name="ai-spawning-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can use the following AI flow graph nodes to spawn AI agents\. An archetype entity is based on a regular entity and specifies individual parameter values for that entity\. If the value of an archetype entity parameter is changed, all instances of that archetype entity in the level are updated automatically\.
+ **Entity:SpawnArchetype** 
+ **Entity:Spawn** 

**To access Flow Graph nodes**

1. In the Rollup Bar , click **AI**, **TagPoint**, and then enter a name\.

1. In the current level, click to place the tag point\.

1. Right\-click the tag point, click **Create Flow Graph**, and enter a name\.

1. In Lumberyard Editor, click **Tools**, **Other**, **Flow Graph**\.

1. In **Flow Graph**, under **Flow Graphs**, select the new flow graph just created\.

1. Right\-click anywhere in the graph, click **Add Node**, and then click to create the following nodes:

   1. **Game:Start**

   1. **Entity:SpawnArchetype**

   1. **Entity:EntityPos**

1. Drag node outputs to node inputs to create the following links:

   1. **Game:Start** output links to **Entity:SpawnArchetype Spawn**

   1. **Entity:EntityPos** pos links to **Entity:SpawnArchetype Pos**

   1. **Entity:EntityPos** rotate links to **Entity:SpawnArchetype Rotate**

   1. **Entity:EntityPos** scale links to **Entity:SpawnArchetype Scale**

1. For **Entity:SpawnArchetype**, click **Archetype** and make a selection from the menu\.

1. For **Entity:EntityPos**, right\-click **Choose Entity**, click **Assign graph, entity, <Graph Entity>**, and enter the name of the tag point created in step 6\.