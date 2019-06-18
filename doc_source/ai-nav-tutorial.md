# Tutorial: Basic AI Navigation<a name="ai-nav-tutorial"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

This tutorial covers basic AI agent navigation through a level\. A tagpoint is used to obtain the destination location within the navigation area\. 

The position coordinates for the TagPoint are dynamic, meaning you can move the TagPoint around and the AI updates its new destination coordinates accordingly\. 

**To make an AI agent navigate**

1. In the Rollup Bar, on the **Objects** tab, click **AI**, **NavigationArea**\.

1. In the level, click to define boundary nodes for the navigation area, then double\-click to complete\.

1. In the Rollup Bar, click **AI**, **TagPoint**, then click to place it in the level\.

1. In the Rollup Bar, click **Entity**, **AI**, select your asset, and then click to place it in the level\.

1. In the Rollup Bar, click **Entity, Default, FlowgraphEntity**, then click to place it in the level\.

1. In the level, right\-click the flow graph entity, click **Create Flow Graph**, and name it\.

1. In the Flow Graph editor, under **Flow Graphs**, select the flow graph entity\.

1. Right\-click anywhere in the graph, click **Add Node**, and create the following nodes:

   1. **Game:Start**

   1. **AISequence:Start**

   1. **AISequence:Move**

   1. **AISequence:End**

   1. **Entity:EntityPos**

1. Click and drag to create links between the outputs and inputs of the nodes as follows:

   1. **Game:Start** output to **AISequence:Start** Start

   1. **AISequence:Start** Link to **AISequence:Move** Start

   1. **AISequence:Move** Done to **AISequence:End** End

   1. **Entity:EntityPos** pos to **AISequence:Move** Position

1. For each of the three **AISequence nodes**, do the following:

   1. Select the entity in the entity tree to assign it\.

   1. Right\-click the top bar of the node\.

   1. click **Assign Selected Entity, Choose Entity**\.

   1. Enter the name of the AI agent selected\.

1. For the **Entity:EntityPos** node, do the following: 

   1. Select the tagpoint in the entity tree\.

   1. Right\-click the entity top bar of the node\.

   1. Click **Assign Selected Entity, Choose Entity**\.

   1. Enter the name of the tagpoint\.

1. Press Ctrl\+G to test the AI agent navigation to the tagpoint\.