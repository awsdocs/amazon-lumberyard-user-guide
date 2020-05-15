# Common Tasks, EBuses, and Handlers<a name="ebuses-tasks-handlers"></a>

The following are some common game programming tasks and the EBuses and handlers that you can use to implement them\.

## Detect Mouse, Keyboard, or Other Button Events<a name="ebuses-tasks-handlers-detect-mouse-keyboard-events"></a>


****  

|  |  | 
| --- |--- |
| Bus | AZ::InputEventNotificationBus | 
| Events | OnPressed, OnHeld, OnReleased | 
| File | InputEventBus\.h | 

Use these events to detect when mouse, keyboard, or other buttons are pressed, held, or released\.

## Detect Entity or Component Readiness<a name="ebuses-tasks-handlers-detect-component-readiness"></a>


****  

|  |  | 
| --- |--- |
| Bus | LmbrCentral::MeshComponentNotificationBus | 
| Events | OnMeshCreated, OnMeshDestroyed | 
| File | MeshComponentBus\.h | 

Even after an entity has been created and its components have been activated, visual data might not be fully loaded\. The `OnMeshCreated` event occurs when the mesh creation is complete\. This is useful if you want to access the underlying `ICharacterInstance` and `ISkeletonAnim` members in order to play animations\. More generally, it is useful to declare a component or entity as "alive" or game ready, whatever that might mean for your application\.

## Detect When a Member Joins or Leaves a Session<a name="ebuses-tasks-handlers-detect-session-events"></a>


****  

|  |  | 
| --- |--- |
| Bus | GridMate::SessionEventBus | 
| Events | OnMemberJoined, OnMemberLeaving | 
| File | Session\.h | 

You can use the `SessionEventBus` to detect when a member joins or leaves a network session\. For documentation on this EBus, see [Reacting to Session Events](network-session-service-events.md) in the [Using Lumberyard Networking](network-intro.md)\.

## Get and Set Physics Characteristics<a name="ebuses-tasks-handlers-physics-characteristics"></a>


****  

|  |  | 
| --- |--- |
| Bus | LmbrCentral::PhysicsComponentRequestBus | 
| Methods | AddImpulse, GetMass, SetMass, GetVelocity, SetVelocity, etc\. | 
| File | PhysicsComponentBus\.h | 

The `PhysicsComponentRequestBus` contains useful methods for getting or setting the physical characteristics of objects like mass, density, velocity, and water damping\. For an example of using a pointer directly to the underlying handler for better access to functions such as `GetVelocity`, see [Direct Access to EBus Handlers](ebus-handlers-direct-access.md)\.

## Get Notifications for Animation Events<a name="ebuses-tasks-handlers-animation-events"></a>


****  

|  |  | 
| --- |--- |
| Bus | LmbrCentral::CharacterAnimationNotificationBus | 
| Event | OnAnimationEvent | 
| File | CharacterAnimationBus\.h | 

If you have set up animations in the `.animevents` file in Geppetto, an `OnAnimationEvent` event is called for each animation event during animation playback\. You can monitor this to get notifications for animation events\. The string configured for the animation event in Geppetto is held in the `LmbrCentral::AnimationEvent::m_animName` variable\.

## Get or Set the Location of an Entity in the World<a name="ebuses-tasks-handlers-entity-location"></a>


****  

|  |  | 
| --- |--- |
| Bus | AZ::TransformBus | 
| Methods | GetWorldX, SetWorldX, GetWorldY, SetWorldY, etc\. | 
| File | TransformBus\.h | 

The `TransformBus` contains many useful methods for getting or setting where in the world the entity is, such as xyz axis locations\. For an example of using a pointer directly to the entity's transform for more optimal access to functions such as `GetBasisY` \(the entity's forward vector\), see [Direct Access to EBus Handlers](ebus-handlers-direct-access.md)\.

## Manually Play Animations<a name="ebuses-tasks-handlers-play-animations"></a>


****  

|  |  | 
| --- |--- |
| Bus | LmbrCentral::SkinnedMeshComponentRequestBus | 
| Method | GetCharacterInstance | 
| File | SkinnedMeshComponent\.h | 

To play animations manually, use the `ISkeletonAnim` in the character instance\. To get the `ISkeletonAnim` from the `ICharacterInstance`, use `ICharacterInstance::GetISkeletonAnim()`\.

## Use an EBus from Another Component<a name="ebuses-tasks-handlers-use-other-component-ebus"></a>


****  

|  |  | 
| --- |--- |
| Bus | AZ::EntityBus | 
| Events | OnEntityActivated, OnEntityDeactivated | 
| File | EntityBus\.h | 

The `OnEntityActivated` and `OnEntityDeactivated` events are called after all of an entity's components have had their `Activate()` or `Deactivate()` function called\. These events can be useful if you want your component to use an EBus that another component has already set up in its `Activate()` function\.

## Use Tick Events<a name="ebuses-tasks-handlers-tick-events"></a>


****  

|  |  | 
| --- |--- |
| Bus | AZ::TickBus | 
| Event | OnTick | 
| File | TickBus\.h | 

A tick is a unit of time generated by the component application\. The `OnTick` event signals that the application has issued a tick and is called each frame\. By default, handlers receive events based on the order in which the components are initialized, but you can override this\. For more information, see [Tick Bus and Components](component-entity-system-pg-tick-bus.md)\.