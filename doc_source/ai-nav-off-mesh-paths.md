# Using AI Paths for Navigation<a name="ai-nav-off-mesh-paths"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

An AI path is a control object that is used to guide an AI agent from point to point along a specified route in a level\. AI paths are useful for AI agents that need to traverse between two navigation meshes\. 

**To create an AI Path**

1. In the Rollup Bar, click **AI**, **AIPath**\.

1. Under **AIPath Params**, set properties and parameter values as needed:

   1. **Road** – Used for** CRoadNavRegion::CreateRoad** and road navigation\. Links with other nearby roads for land\-based vehicles\.

   1. **ValidatePath** – If enabled, the path displays validation information when selected\.

   1. **Closed** – If true, the path is a loop\.

1. Click **File**, **Export to Lumberyard**\. This is a necessary step for the navigation system\.

Unless absolutely necessary, AI path navigation should be Uninterruptable, meaning nothing should disrupt or block an AI agent moving along a path\.

**To set AI Path movement as uninterruptible**

1. In Lumberyard Editor, click **Tools**, **Flow Graph**\.

1. Under **Graphs**, **Global**, **AI actions**, select the AI agent\.

1. In the **AISequence:Start** node, clear the **Interruptible** check box\. 

You can add an AI Path to Flow Graph logic as follows:

**To add an AI Path to Flow Graph**

1. In Flow Graph, under **Graphs**, **Level**, **Entities**, select the applicable flow graph\.

1. Right\-click anywhere in the graph, and then click **Add Node**, **AISequence**, **MoveAlongPath**\.

1. In the **AISequence:MoveAlongPath** node, for **PathName**, enter the name of the AI Path value from the Rollup Bar\.