# Flow Graph<a name="component-flowgraph"></a>


****  

|  | 
| --- |
| Component entity system is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

Component entities support some flow graphs using the context menu on selected component entities\.

The following flow graph nodes are supported for component entities:
+ **Movement:RotateEntity** – Applies a rotation velocity to an entity\.
+ **Movement:MoveEntityTo** – Moves the entity to the specified location\.
+ **ComponentEntity:TransformComponent:GetEntityPosition** – Returns the entity's position\.
+ **ComponentEntity:TransformComponent:GetEntityRotation** – Returns the entity's orientation\.
+ **ComponentEntity:TransformComponent:SetEntityPosition** – Specifies the entity's position\.
+ **ComponentEntity:TransformComponent:SetEntityRotation** – Specifies the entity's rotation\.
+ **ComponentEntity:TriggerComponent:EnterTrigger** – Triggers event notification on entry or exit\.

A few things to note about component entities and flow graph:
+ After you add a flow graph to the entity, you can access the flow graph from the **Flow Graph** editor in the **Graphs** pane under **FlowGraph Components**\.
+ Component entities support multiple flow graphs\. You can add, remove, or open a flow graph from the viewport using the context menu\.
+ Flow graph context menus also work on multiple selected entities\.

**To add a flow graph component to an entity**

1. In the viewport select an existing entity\.

1. Right\-click the entity, and click **FlowGraph**, **Add**\.

1. Enter a name for the flow graph\.