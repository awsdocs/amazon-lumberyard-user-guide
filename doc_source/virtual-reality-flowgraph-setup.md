# Setting Up a Basic Virtual Reality Flow Graph<a name="virtual-reality-flowgraph-setup"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

The following  examples guide you through a basic setup of a virtual reality level and its accompanying head\-mounted display\(s\)\.

When you create a new level, the default point of origin is 0,0,0—the location at which the level starts during gameplay\. You can specify a custom starting point by [placing a camera](cinematics-cameras-intro.md) at a specific location and enabling it with flow graph\.<a name="vr-flowgraph-specify-a-starting-point"></a>

**To specify a custom starting point**

1. Place a [game play camera](cinematics-cameras-intro.md) at the desired location in your level\. This is your default camera\.

1. Right\-click the camera entity and click **Create Flow Graph** to open the **Flow Graph** editor\.

1. Drag a **Game:Start** node and **Camera:View** node onto your flow graph canvas\.

1. Connect the **Game:Start** node's **output** output to the **Camera:View** node's **Enable** input\.

1. Right\-click **Choose Entity** and click **Assign graph entity**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-1.png)

During virtual reality gameplay, a player may need to recenter their gameplay world around themselves, and start from a known position in space, regardless of their current position\. Using flow graph, you can add a keyboard shortcut that the player can use to accomplish this\.

**To add a keyboard shortcut for recentering**

1. Open the Flow Graph editor\.

1. Drag a **Debug:InputKey** node and **VR:RecenterPose** node onto the canvas\.

1. Connect the **Debug:InputKey** node's **Pressed** output to the **VR:RecenterPose** node's **Activate** input\.

1. On **Debug:InputKey** node, click on **Key=** and set the key to the shortcut key you want to use\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-2.png)

For your virtual reality game, you may want to place a graphical, virtual controller to represent where a physical controller is within the 3D space\. You can use flow graph to add this graphical representation of a controller \(for example, hands, weapons, and so on\)\.

For this procedure, the default camera is the gameplay camera that you placed in the [custom starting point](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/vr-flowgraph-specify-a-starting-point.html) procedure\. Assigning the default camera entity to the **VR:ControllerTracking** node ensures that the motion controllers are aligned in the same space\.

**To add virtual controllers and assign the default camera**

1. In the Perspective viewport, select the default camera\. 

1. In **Flow Graph** editor, drag the **VR:ControllerTracking** node onto the flow graph canvas\.

1. Right\-click **Choose Entity** and click **Assign Graph Entity**\.

1. In the **Perspective** viewport, place one or more entities that you want to use as controllers into your level\. Ensure that you keep the entity selected\.

1. In the **Flow Graph** editor, drag one or two **Entity:EntityPos** nodes onto your flow graph canvas\.

1. On the **Entity:EntityPos** node, right\-click **Choose Input** and click **Assign selected entity**\.

   If you placed another entity that you want to assign as the other controller, select the entity and repeat this step for the other **Entity:EntityPos** node\.

1. Connect **VR:ControllerTracking** node's **Left Pos** output to the **Entity:EntityPos** node's **pos** input\.

1. Connect **VR:ControllerTracking** node's **Left Rot \(PRY\)** output to the **Entity:EntityPos** node's **rotate** input\.

1. Repeat the previous two steps for the **Right Pos** and **Right Rot \(PRY\)**, if applicable\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-3.png)