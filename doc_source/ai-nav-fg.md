# Using Flow Graph for AI Navigation<a name="ai-nav-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

Flow graphs are a visual way to define AI navigational logic by creating and linking navigation nodes together\. Flow Graph is accessed from Lumberyard Editor by clicking **Tools**, **Flow Graph**\. 

Some of the navigation\-related nodes are:

**AISequence:Animation ** – Moves the AI to a location using a specified animation for the defined Stance, and plays an animation once the target has been reached\.

**AISequence:ApproachAndEnterVehicle ** – Moves the AI agent to and then inside a vehicle, using a specified animation for the supplied Stance\.

**AISequence:Move ** – Moves the AI to a location using a specified animation for the supplied Stance\.

**AISequence:MoveAlongPath ** – Moves the AI along a path indicated by the supplied PathName, using the appropriate animations for the supplied Stance\.

**Movement:MoveEntityTo** – Moves the AI along a path indicated by the supplied PathName, using the appropriate animations for the supplied Stance\.

**AI:RayCastMNM** – Performs a raycast to the AI multilayer nav mesh relative to an entity\.

**AI:RegenerateMNM ** – Regenerates the mesh at specified minimum and maximum positions\. This is useful after the terrain has changed or an object has moved\.

**Vehicle:ChaseTarget ** – Moves the vehicle along a defined off\-mesh path, following a target vehicle and attempting to maintain a line of sight\.

**Vehicle:FollowPath ** – Moves the vehicle along a defined off\-mesh path at a specified speed\.