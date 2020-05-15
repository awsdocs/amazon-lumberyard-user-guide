# Navigation<a name="component-navigation"></a>


****  

|  | 
| --- |
| Component entity system is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

Use the **Navigation** component on an AI entity for pathfinding and pathfollowing functionality\. The **Navigation** component supports AI and other game logic by accepting navigation commands and dispatching movement requests\. 

**Topics**
+ [Example: Navigation Procedure](#component-navigation-example)
+ [Navigation Component Properties](#component-navigation-properties)
+ [EBus Request Bus Interface](#component-navigation-ebusrequest)
+ [EBus Notification Bus Interface](#component-navigation-ebusnotification)

## Example: Navigation Procedure<a name="component-navigation-example"></a>

The following example demonstrates how you can use the **Navigation** component\. You can find the assets used in this procedure in the [Starter Game Sample](sample-level-starter-game.md) project\.

**To use the Navigation component**

1. Create a [navigation area](component-nav-area.md)\.

1. Create an entity named **box**, and then do the following:

   1. Add a **[Mesh](component-static-mesh.md)** component to the entity\.

   1. For its **Mesh asset**, select an object in the `StarterGame\Objects` directory\.

   1. [Move](lumberyard-editor-toolbars.md#lumberyard-editor-toolbars-editmode) the object to a corner of your navigation area\.

1. To add a character, in the **[Asset Browser](asset-browser-intro.md)**, in the `StarterGame\slices` directory, drag **playerslice\.slice** to your viewport and then move the character to a different corner of your navigation area\.

1. In the **Entity Outliner**, expand **PlayerSlice** and select the **Jack** entity\.

1. In the **Entity Inspector**, do the following: 

   1. From the **AI** section, add a **Navigation** component to **Jack**\.

   1. In the **Navigation** component's [**Agent Type**](component-nav-area.md#component-nav-area-properties-agent-types), ensure that **MediumSizedCharacters** is selected\.

      This tells the navigation system that this character follows navigation paths as a medium\-sized character\.

   1. From the **Scripting** section, add a [**Lua Script**](component-lua-script.md) component to **Jack**\.

   1. For **Script**, add the following Lua script\. 
**Note**  
To create a Lua script, copy and paste the following text into a text file, and then change the `.txt` extension to `.lua`\. Place the file in your game project directory so that you can select it in your level\.

      ```
      local navigationmoversimplified =
      {
          -- Adds properties to the Entity Inspector for easy setup of initial values.
          Properties =
          {
              -- This is the target toward which you'll move
              MoveToEntity = {default=EntityId(), description="Entity to move to."},
          }
      }
      
      function navigationmoversimplified:OnActivate()
      
      	self.entityBus = EntityBus.Connect(self, self.Properties.MoveToEntity);
          
      end
      
      function navigationmoversimplified:OnEntityActivated(remoteEntity)
      
          -- Move!
          self.requestId = NavigationComponentRequestBus.Event.FindPathToEntity(self.entityId, self.Properties.MoveToEntity)  
          
      end
      
      return navigationmoversimplified
      ```

   1. In the Lua Script's **MoveToEntity** property, click the target icon ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/picker.png) and in the **Entity Outliner**, select **box**\. The text **box** appears in the **MoveToEntity** box\. 

      The script subscribes to the `OnEntityActivated` event for the remote entity specified \(in this case, the box\), and tells **Jack** character to move toward the remote entity when the remote entity is spawned\.

1. Divide the navigation mesh into separate chunks, leaving a path between them\. To block the character from traveling to the box in a straight line, do

    one of the following:
   + [Create an exclusion area](component-nav-area.md#component-nav-area-exclusion)
   + [Place a static object](component-nav-area.md#component-nav-area-static-entities)

   The following example setup uses a static object\.  
![\[Character, box, and obstacle setup for navigation\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-navigation-example.png)

1. Press **Ctrl\+G** to play the game\. Without any player input, the **Jack** character should move toward the opening in the navigation mesh and then toward the box\. Press **Esc** to quit\.
**Note**  
If **Jack** moves too slowly, specify a higher value in the **Navigation** component's **Agent Speed** property to increase his speed\.

1. You can also do the following:
   + Make a complex path using exclusion areas, static objects, and [terrain modifications](terrain-intro.md)\.
   + Modify the static object to block Jack's path completely\. Note that he does not move toward the target, because there isn't a path\.

## Navigation Component Properties<a name="component-navigation-properties"></a>

The **Navigation** component has the following properties:

**Agent Type**  
Specifies this AI's entity type for navigation purposes\. Defining the agent type determines which [navigation area](component-nav-area.md) the entity follows in a scenario where there are different navigation meshes for larger vehicles and smaller humanoid bots\. These agent types are defined in the `lumberyard_version\dev\your_project_name\Scripts\AI\Navigation.xml` file\.  
To define an agent type on your navigation area, see the **[Navigation Area](component-nav-area.md)** component\.

**Agent Speed**  
Sets the speed of the agent while navigating\.  
Default value: `1`

**Agent Radius**  
Sets the entity radius for navigation purposes\. Independent of physics or other collision concerns, the pathfinder uses this value to move around an area with obstacles while cutting corners\.  
Default value: `4`

**Arrival Distance Threshold**  
Sets the minimum distance from an end point when an entity's movement stops and is considered complete\.  
Default value: `0.25` 

**Repath Threshold**  
Sets the minimum distance from the previously known location before an entity's new path is calculated\.  
Default value: `1`

**Move Physically**  
Applies movement through physics\. You must add a **Character Physics** component to the entity for this functionality to work\. We recommend this method to apply movement to a character during pathfollowing because it handles uneven terrain and character limitations properly\. If deselected, movement applies directly to the entity's transform\.  
Default value: `true`

## EBus Request Bus Interface<a name="component-navigation-ebusrequest"></a>

Use the following request functions with the `NavigationComponentRequestBus` event bus \(EBus\) interface to communicate with other components of your game\.

For more information about using the EBus interface, see [Working with the Event Bus \(EBus\) System](ebus-intro.md)\.

### FindPath<a name="navigation-ebus-findpath"></a>

Finds a requested path configuration\.

**Parameters**  
`request` – Allows the issuer of the request to override one, all, or none of the pathfinding configuration defaults for this entity\.

**Return**  
A unique identifier for this pathfinding request\.

**Scriptable**  
No

### FindPathToEntity<a name="navigation-ebus-findpathtoentity"></a>

Creates a pathfinding request to navigate toward the specified entity\.

**Parameters**  
`EntityId` – ID of the entity toward to which you want to navigate\.

**Return**  
A unique identifier for the pathfinding request\.

**Scriptable**  
Yes

### Stop<a name="navigation-ebus-stop"></a>

Stops all pathfinding operations for the provided `requestId`\. Use the ID to ensure that the request you want to cancel is the request that is currently processing\. If the specified `requestId` is different from the ID of the current request, then the stop command is ignored\.

**Parameters**  
`requestId` – ID of the request to cancel\.

**Return**  
None

**Scriptable**  
Yes

## EBus Notification Bus Interface<a name="component-navigation-ebusnotification"></a>

Use the following notification functions with the `NavigationComponentNotificationBus` event bus \(EBus\) interface to communicate with other components of your game\.

For more information about using the EBus interface, see [Working with the Event Bus \(EBus\) System](ebus-intro.md)\.

### OnSearchingForPath<a name="navigation-ebus-onsearchingforpath"></a>

Indicates that the pathfinding request was sent to the navigation system\.

**Parameters**  
`requestId` – ID of the path search request\.

**Return**  
None

**Scriptable**  
Yes

### OnPathFound<a name="navigation-ebus-onpathfound"></a>

Indicates that a path was found for the indicated request\.

**Parameters**  
`requestID` – ID of the found request for the path search\.  
`currentPath` – The path calculated by the pathfinder\.

**Return**  
Flag that indicates whether or not to traverse this path\.

**Scriptable**  
No

### OnTraversalStarted<a name="navigation-ebus-ontraversalstarted"></a>

Indicates that traversal for the indicated request has started\.

**Parameters**  
`requestId` – ID of the request for which traversal has started\.

**Return**  
None

**Scriptable**  
Yes

### OnTraversalInProgress<a name="navigation-ebus-ontraversalinprogress"></a>

Indicates that traversal for the indicated request is in progress\.

**Parameters**  
`requestId` – ID of the request for which traversal is in progress\.

**Return**  
None

**Scriptable**  
Yes

### OnTraversalComplete<a name="navigation-ebus-ontraversalcomplete"></a>

Indicates that traversal for the indicated request completed successfully\.

**Parameters**  
`requestId` – ID of the request for which traversal has completed\.  
`distanceRemaining` – The remaining distance in the path\.

**Return**  
None

**Scriptable**  
Yes

### OnTraversalCancelled<a name="navigation-ebus-ontraversalcancelled"></a>

Indicates that traversal for the indicated request was canceled before completing successfully\.

**Parameters**  
`requestId` – ID of the request for which traversal was canceled\.

**Return**  
None

**Scriptable**  
Yes