# Script Canvas Script Events<a name="script-canvas-script-events"></a>

In Lumberyard, scripts can communicate with each other by using script events\. To author script events, use the Asset Editor or Lua\. Script Canvas and Lua can send or receive the events that you create\. In Script Canvas, you can add nodes that send or receive script events\. Events sent from Script Canvas can be handled in Lua\. Likewise, events sent from Lua can be handled in Script Canvas\. 

## Prerequisites<a name="script-canvas-script-events-prerequisites"></a>

To use script events, you must enable the **Script Events** gem in your project\. For information about enabling gems, see [Enabling Gems](gems-system-using-project-configurator.md)\.

## Creating Script Events in Script Canvas<a name="script-canvas-script-events-creating-in-script-canvas"></a>

In Lumberyard Editor, you can create script events by using the Asset Editor\.

**To create a script event**

1. In Lumberyard Editor, choose **Tools**, **Asset Editor**\.  
![\[Choose Tools, Asset Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-1.png)

1. In the **Asset Editor**, choose **File**, **New**, **Script Events**\.  
![\[Choose File, New, Script Events in the Asset Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-2.png)

1. In the **Asset Editor**, enter the information that defines the script event\.  
![\[Creating a script event in the Asset Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-3.png)  
**Script Event Properties**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/script-canvas-script-events.html)  
**Event Properties**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/script-canvas-script-events.html)  
**Parameter Properties**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/script-canvas-script-events.html)

1. Choose **File**, **Save**, or press **Ctrl\+S**\.

1. In the **Save As** dialog box, enter a file name for your `.scriptevents` file, and click **Save**\. 
**Note**  
To ensure that the script event asset saved correctly, check the bottom of the Asset Editor for the message "`file_name.scriptevents` \- Asset loaded\!" message \. If you see the error message Failed to save asset due to validation error, check the Lumberyard Editor **Console** window or the `lumberyard_version\dev\Cache\project_name\pc\user\log\Editor.log` file for more information\. 

## Using Script Events in Script Canvas<a name="script-canvas-script-events-using-in-script-canvas"></a>

Script Canvas scans for and detects script event assets, so after you define a script event, you can use it in Script Canvas\.

### Script Events in the Node Palette<a name="script-canvas-script-events-node-palette"></a>

Script event assets appear by default in the **Script Events** category in the Script Canvas editor **Node Palette**\.

![\[The Script Events category in the Script Canvas Node Palette.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-4.png)

**Note**  
To change the name of the category, open the script event's asset definition in the Asset Editor and edit the `Category` property\.

### Sending Events<a name="script-canvas-script-events-sending"></a>

You can send an event by adding a **Send** *method\_name* node to a Script Canvas graph\.

**To send an event**

1. Drag and drop the method that you want to send onto the Script Canvas graph\.

1. In the context menu, choose **Send** *method\_name*\.  
![\[Choose Send method_name in the context menu.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-5.png)

   A method send node is added to the graph\.  
![\[A send node added to a Script Canvas graph.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-6.png)

1. Connect this node to the appropriate logic and data inputs\. When the Script Canvas graph runs, it sends the event to the entities or systems to which the node is connected\.

### Handling Events<a name="script-canvas-script-events-handling"></a>

You can handle an event by adding a **Receive** *method\_name* node to a Script Canvas graph\.

**To handle an event**

1. Drag and drop a script event method onto the canvas\.

1. In the context menu, choose **Receive** *method\_name*\.  
![\[Choose Receive method_name in the context menu.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-7.png)

   An event handler method node is added to the graph\.  
![\[A receive node added to a Script Canvas graph.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-8.png)

1. Connect your event handling logic to the **Out** pin of the node\.

1. Connect the data pin as needed\.

## Script Events Best Practices<a name="script-canvas-script-events-best-practices"></a>

The following are some best practices for using script events in Script Canvas\.

### Ensure Entities are Activated Before Events are Sent<a name="script-canvas-script-events-ensure-entity-activation-before-sending"></a>

Sending events during entity activation can have undesired results\. Because the order of activation of entities is not guaranteed, when an event is sent during activation, some entities that need to handle the event might not receive it\. In particular, the **On Graph Start** and **On Entity Activated** nodes are subject to activation order issues\. Be careful when sending events from them\.

To ensure that all entities that need to listen for and handle a given script event are ready to receive the event, queue the message on the [tick bus](component-entity-system-pg-tick-bus.md)\. One way to implement this strategy is to connect the **On Graph Start** node to a **Tick Delay** node\. The delay helps to ensure that when a script event message is sent, all entities that could possibly be connected to that script event receive the event\.

![\[Using the Tick Delay node in Script Canvas to ensure that entities are activated before events are sent.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/script-canvas-script-events-9.png)

### Be Aware of Script Event Asset Versioning<a name="script-canvas-script-events-asset-versioning"></a>

Because Script Events are user\-created assets, problems can occur when an asset that is referenced in existing scripts or Script Canvas graphs changes\.

Script Canvas provides Script Event version validation\. When a Script Event asset is modified, Script Canvas updates the Script Event nodes that reference it\. If you open a graph that has a Script Event that has been modified, the graph is marked as modified\. To update the Script Event nodes to their latest versions, save the graph\.

### Use Script Events Instead of the Gameplay Notification Bus System<a name="script-canvas-script-events-gameplay-notification-bus-system-deprecation"></a>

Script events offer the following advantages over the [gameplay bus](component-entity-system-gameplay-bus.md) system\. Script events:
+ Are data driven\.
+ Support more data types\.
+ Require less maintenance\.
+ Can be used in both Script Canvas and Lua\.

For these reasons, script events supersede the gameplay notification bus system and the following `GameplayNotificationBus` related classes:
+ `GameplayNotificationBus`
+ `GameplayNotificationId`
+ `BehaviorGameplayNotificationBusHandler`
+ `GameplayEventHandlerNode` \(Legacy\)

#### Migrating to Script Events<a name="script-canvas-script-events-migrating-to"></a>

If your project uses `GameplayNotificationBus`, you can modify it to use script events\.

**To migrate from GameplayNotificationBus to script events**

1. Create a new Script Event that performs the event messaging that you require\.

1. Identify the Script Canvas graphs that use `GameplayNotificationBus`\.

1. Replace the nodes that use `GameplayNotificationBus` with either a Script Event **Send** or a Script Event **Receive** node\.