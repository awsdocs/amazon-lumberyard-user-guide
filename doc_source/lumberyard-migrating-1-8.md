# Lumberyard 1\.8<a name="lumberyard-migrating-1-8"></a>

In Lumberyard 1\.8, the [Behavior Context](component-entity-system-reflection-behavior-context.md) replaces the script context\. The behavior context works with [serialize context](component-entity-system-reflect-component.md), [edit context](component-entity-system-reflect-component.md), and [network context](component-entity-system-reflect-component.md) to provide rich C\+\+ reflection\. Behavior context focuses on the runtime aspects of C\+\+ code and allows you to manipulate C\+\+ code and objects while they are created\. All script bindings, including Lua, use this reflection\. Reflection is also used to modify objects while in running state \(such as animating object properties\) and read current properties for component state transitions\. You can have multiple behavior contexts that are specialized for different purposes, and you can unreflect the behavior contexts in order to implement reloading\. With the introduction of behavior context, you can no longer reflect directly into the script context\.

After upgrading your projects to Lumberyard 1\.8, do the following to migrate your existing projects into the behavior context format:

1. Convert your C\+\+ code from the script context to the behavior context\.

1. Convert your Lua script syntax\.

## Converting C\+\+ Code from the Script Context to the Behavior Context<a name="lumberyard-migrating-1-8-code"></a>

The script context is still used to manage a Lua VM instance; however, it now binds to a behavior context instance\. The behavior context uses the property, method, class, EBus, and attributes primitives\. For more information, see [Behavior Context](component-entity-system-reflection-behavior-context.md)\. You must convert any event buses that expose functionality to Lua using the script context\.

**To convert your C\+\+ code from the script context to the behavior context**

1. Convert any EBus senders to behavior context handlers\.

1. Use the behavior context in your component's `Reflect` method to expose the EBus handlers to Lua\. 

1. Remove the old `AZ_SCRIPTABLE_EBUS` macro calls\.

### Migrating Globals, Classes, and EBus<a name="lumberyard-migrating-script-context-to-behavior-context"></a>

You can see all support script attributes in `AZ::Script::Attributes`, for example `Storage`, `MethodOverride`, `ConstructorOverride`, and `Operator`\. This section includes examples for certain migrations\.

You can use the same method as before in order to implement generic functionality, such as accepting any number and type of arguments\. The script context binding to the behavior context provides some automation\. For example, if a function signature accepts `ScriptDataContext` as the last parameter, the signature always uses that function\. Instead of unpacking the arguments from the script VM, it wraps the arguments in `ScriptDataContext` and allows you to handle the arguments directly\.

Method

Conversion is required for methods if you use class operators or have default values, as in the following example\. 

```
scriptContext.Method("GlobalFunction",&GlobalFunction, scriptContext.DefaultValues(555), "Method description for authors");behaviorContext.Method("GlobalFunction",&GlobalFunction, BehaviorMakeDefaultValues(555),
      "Method description for authors");
```

Fields

Fields are no longer supported\. Each value is now a property that you can control\. Read/write values are determined with setters and getters, as in the following example\. 

```
scriptContext.Field("globalField", &s_globalField);behaviorContext.Property("globalField", BehaviorValueProperty(&s_globalField));
```

Attributes

In the behavior context, both methods and properties support attributes\. Because the behavior context is more generic, you may want to reflect a C\+\+ function for C\+\+ calls like animating a value\. You may also want to have a different function for the script context\. You can reflect the function that you used to reflect only to the script context\. The following script attribute is still supported\. 

```
scriptContext.Method("MethodFooForScriptOnly",&MethodFooForScriptOnly);behaviorContext.Method("MethodFoo",&MethodFoo)
```

**Classes**  
Classes are generic and no longer require specific ownership or default constructors during class declaration\. These values have been moved to attributes\.

Constructors

Similar to methods, the script context provides automation with constructors by using the `ScriptDataContext` parameter and applying the same operations for a method\. By default, script owns any objects that are created in script\. C\+\+ runtime owns any objects that are passed into script\. You can change this behavior by using the `Acquire` or `Release` functions in C\+\+ or Lua\. The `MyClass` example below has a `MyClass(int)` constructor and a custom allocator/deallocator and is owned by script\. You can provide the class name; however, by default the `AzTypeInfo` is used to determine the class name\. You can specify the `int` argument for constructor to include as many as you want\.

```
scriptContext.Class<MyClass, void(int), ScriptContext::SP_RAW_RUNTIME_OWN>("MyClass", &MyClassAllocate, &MyClassDestructor)->
        ... methods, enums, constants and properties
behaviorContext.Class<MyClass>() 
        ->Constructor<int>()   
        ->Allocator(&MyClassAllocate, &MyClassDestructor)
        ... methods, enums, constants and properties
  
// If the class is passed by value
scriptContext.Class<MyValueClass, ScriptContext::SP_VALUE>("MyValueClass")
        ... methods, enums, constants and properties
behaviorContext.Class<MyValueClass>()
        ->Attribute(AZ::Script::Attributes::Storage,AZ::Script::Attributes::StorageType::Value)
        ... methods, enums, constants and properties
  
// Operators are script/Lua-specific and are now moved to attributes
scriptContext.Class<Uuid, void (ScriptDataContext&), ScriptContext::SP_VALUE>("Uuid")
        ->Operator(ScriptContext::OPERATOR_TOSTRING, &Uuid::ToString)
        ...
behaviorContext.Class<Uuid>() 
        ->Attribute(AZ::Script::Attributes::Storage,AZ::Script::Attributes::StorageType::Value)     
        ->Method("ToString",&Uuid::ToString)
            ->Attribute(AZ::Script::Attributes::Operator,AZ::Script::Attributes::OperatorType::ToString)
        ...
```

EBus

Migrating the EBus binding requires different steps than methods and classes\. See the following EBus class `MyEvents` example for more information\. 

```
// EBus class MyEvents : public AZ::EBusTraits
{
    float OnEvent(float a, float b) = 0;
};
  
using MyEBus = AZ::EBus<MyEvents>;
  
// Script context
AZ_SCRIPTABLE_EBUS(
        MyEBus ,   // Generates class MyEBusHandler
        MyEBus ,   // Generates class MyEBusSender
        "{8165B431-DEAB-4033-984C-2400A74C69F8}", // Handler type UUID
        "{6B160DDE-36CB-4876-B09D-E848503C7AE0}", // Sender type UUID
        AZ_SCRIPTABLE_EBUS_EVENT_RESULT(float,0.0f,OnEvent, float, float) // Reflects an event with result float; the default result is 0.0f. The "OnEvent" name must match and has two float parameters.
)
  
// Reflecting the EBus (usually a component reflect function) required a call ScriptableEBus_MyEBus::Reflect(scriptContext).
  
// In Lua the code appeared as follows
-- To send messages
myEBusSender = MyEBusSender()
result = myEBusSender:OnEvent(10.0,20.0) -- call on event
  
-- To listen to messages
MyEBusHandlerTable = {
    OnEvent = function(self,a,b)
        -- do something
        return result;
    end
};
  
myEBusHandler = MyEBusHandler(MyEBusHandlerTable /* or , ID when the bus has an ID */);
  
-- To prevent disconnection
myEBusHandler:Disconnect()
  
// The implementation above had a sender that required an ID (0 for no ID) and did not support broadcast versus event or queuing of any events functions.
// In addition, when the event returned const ClassX& it was necessary to implement the class without the macros in order to create temporary storage and return that as a reference.
  
// With the behavior context, sender is no longer required and the handler is written as an EBus listener.
// Note that a sender and handler are not required and you can provide either depending on your requirements.
// It is common to have one bus for requests and one bus for notifications. This pattern is used in most components.
  
// MyEBus behavior context handler class
class MyEBusBehaviorHandler : public MyEBus::Handler, public AZ::BehaviorEBusHandler
{
public:
    AZ_EBUS_BEHAVIOR_BINDER(MyEBusBehaviorHandler, "{19F5C8C8-4260-46B1-B624-997CD3F10CBD}", AZ::SystemAllocator, // Helper macro to set the handler type ID and allocator
                                OnEvent); // Comma-separated names of events to handle
  
    float OnEvent(float a, float b) override   // Implements MyEBus::Handler OnEvent
    {
        float result = 0.0f; // Sets the default value for the result if CallResult doesn't call anything
        CallResult(result, FN_OnEvent, a, b); // FN_OnEvent is generated from the macro above. You can cache the function index if you want static int eventIndex = GetFunctionIndex("OnEvent"); CallResult(result,eventIndex,a,b); if you prefer
        return results;
    }  
};
  
// Wherever you reflect the EBus (usually a component or system component reflect function)
behaviorContext.EBus<MyEBus>("MyEBus")
    ->Handler<MyEBusBehaviorHandler >() // Allows systems that use the behavior context to create handlers for this EBus each time they need to listen for events. You can reflect a bus without a handler so that behavior context users can only send events.
    ->Event("OnEvent",&MyEBus::Events::OnEvent) // Allows the behavior context system to send "OnEvent" events. The code automatically generates Broadcast, Event, QueueBroadcast, QueueEvent, and QueueFunctions if the EBus configuration supports them. You aren't required to provide events; you can provide only a handler if you don't have the behavior context systems to send events.
  
-- In Lua
-- You no longer need to create sender objects. You can send events using the same method as in C++.
result = MyEBus.Broadcast.OnEvent(10.0,20.0) -- Or you can use result = MyEBus.Event.OnEvent(id,10.0,20.0) for issues on an ID, or you can queue events to MyEBus.QueueBroadcast.OnEvent(10.0,20.0)
  
-- To listen
MyEBusHandlerTable = {
    OnEvent = function(self,a,b)
        -- do something
        return result;
    end
};
  
myEBusHandler = MyEBus.Connect(MyEBusHandlerTable) -- You can pass an ID when the bus supports it
  
-- To prevent disconnection
myEBusHandler:Disconnect()
  
// The implementation above is generic. The handler is shared whether you use Lua, Visual Script, or another behavior context-based system. You can now use most of the EBus functionality that is available
// in C++.
```

## Converting the Lua Script Syntax<a name="lumberyard-migrating-1-8-lua"></a>

Several improvements to the Lua syntax provide better flexibility and more similarity to the C\+\+ syntax\. The older script context has been replaced with a new behavior context that provides a more robust EBus script reflection\. As a result, the interfaces for sending events and receiving notifications has changed\. For more information, see [Writing Lua Scripts](lua-scripting-intro.md)\.

### Using Events Instead of Senders<a name="lua-script-senders-events"></a>

With the behavior context, sender objects are no longer used to send events or make requests on an EBus\. You can now send an event directly using an entity ID or EBus as the destination address\. Each bus has a new event table that defines the functions for sending the appropriate events and requests\.

Script context syntax \(previous\):

```
self.uiCanvasLuaBusSender = UiCanvasLuaBusSender(self.canvasEntityId)
local entityWithFader = self.uiCanvasLuaBusSender:FindElementById(2)
local otherEntity = self.uiCanvasLuaBusSender:FindElementById(3)
```

Behavior context syntax \(new\):

```
local entityWithFader = UiCanvasLuaBus.Event.FindElementById(self.canvasEntityId, 2)
local otherEntity = UiCanvasLuaBus.Event.FindElementById(self.canvasEntityId, 3)
```

### Using a Connect Method for Handlers<a name="lua-script-handlers"></a>

The syntax for handlers now uses a `Connect` method that is similar to C\+\+\.

Script context system \(previous\):

```
self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBusHandler(self, canvasEntityId)
```

Behavior context system \(new\):

```
self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBus.Connect(self, canvasEntityId)
```

If you do not want to connect immediately, use the following:

```
self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBus.CreateHandler(self)
```

Then, if you want to connect later, use the following:

```
self.uiCanvasNotificationHandler:Connect(canvasEntityId)
```

### Creating a Local Instance of Your Script Component<a name="lua-script-local-instance"></a>

You can now create a local instance of your script component and return it at the end of the file\. The examples below refer to `MyScriptFile.lua`\.

In the previous script context system, the table name had to match the file name:

```
myscriptfile = {}
```

In the new behavior context system, the table name does not have to match the file name:

```
local ScriptName = {}
```

Use the following Lua script code to return the table that the engine uses\.

```
return ScriptName
```

### Treating Entity References as Any Other Property<a name="lua-script-entity-references"></a>

Entity references no longer use a special syntax and can be treated the same as any other property that contains a reflected type\.

Script context system \(previous\):

```
myscriptfile = {
    Properties = {
        Property = { entity = '' },
    }
}
```

Behavior context system \(new\):

```
local ScriptName = {
    Properties = {
        Property = { default = EntityId() },
        AltProp = EntityId(),
    }
}
 
return ScriptName
```

### Registering to Receive Notifications<a name="lua-script-receive-notifications"></a>

The syntax for registering to receive notifications has changed to use the `Connect()` functions that are defined by each notification bus to connect to a notification bus\. Previously you were required to create a globally defined handler table\. The `Connect()` functions return an object that you must hold in order to disconnect from the notification bus\. You can also use the `CreateHandler()` function to create the handler object and then use the `Connect()` function on that handler object, if you want to separate handler creation from the bus connection\.

Script context system \(previous\):

```
function myscript:OnActivate()
	if self.uiCanvasNotificationHandler == nil then
		self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBusHandler(self, canvasEntityId)
	end
end

function myscript:OnAction(entityId, actionName)
    Debug.Log("Action Notification: " .. entityId.id .. ": " .. actionName)
end
 
function myscript:OnDeactivate()
	if self.uiCanvasNotificationHanlder ~= nil then
		self.uiCanvasNotificationHandler:Disconnect()
		self.uiCanvasNotificationHanlder = nil
	end
end
```

Behavior context system \(new\):

```
function myscript:OnActivate()
	self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBus.Connect(self, canvasEntityId)

end

function myscript:OnAction(entityId, actionName)
    Debug.Log("Action Notification: " .. tostring(entityId) .. ": " .. actionName)
end

function myscript:OnDeactivate()
	if self.uiCanvasNotificationHanlder ~= nil then
		self.uiCanvasNotificationHandler:Disconnect()
		self.uiCanvasNotificationHandler = nil
	end
end
```

Alternate option for the behavior context system \(new\):

```
function myscript:OnActivate()
    self.uiCanvasNotificationHandler = UiCanvasNotificationLuaBus.CreateHandler(self)
    self.uiCanvasNotificationHandler:Connect(canvasEntityId)
end
```

### Passing the EntityId Object<a name="lua-script-entity-ids"></a>

The `.id` property is now deprecated and can no longer be used to access or pass entity IDs\. You can now pass the `EntityId` object\.

### Converting the Main Lua Script Table<a name="lua-script-main-script-table"></a>

Lumberyard Lua scripting is now aligned with standard Lua practices\. Previously the engine could only recognize the main script table if it had the same name as the script file\. Now, the main script table can be local to the file and named as you prefer, as long as the table is returned at the end of the file\.

Script context system \(previous\):

```
myscriptfile = {}          
 
function myscriptfile:OnActivate()
end
 
function myscriptfile:OnDeactivate()
end
```

Behavior context system \(new\):

```
local ScriptName = 
{}

function ScriptName:OnActivate()
end

function ScriptName:OnDeactivate()
end
 
return ScriptName;
```

## Importing FBX Files with Multiple UV Streams<a name="lumberyard-migrating-1-8-multiple-uv-support"></a>

When upgrading to Lumberyard 1\.8, any `.fbx` files that you previously imported in Lumberyard 1\.7 or earlier now imports two UV channels, if present\. Previous versions of Lumberyard imported only the first UV channel\. This can result in an additional, unexpected UV channel on certain meshes\. If you do not want the additional channel, you can use a DCC tool such as Autodesk 3ds Max, Autodesk Maya, or Blender to remove the channel\.

## Converting Material Assets<a name="lumberyard-migrating-1-8-texture-tiling-conversion-script"></a>

Lumberyard 1\.8 introduces a feature called independent texture tiling\. With this feature you can author independent texture modulator values in the second diffuse, emittance, or detail maps\. Lumberyard provides a conversion script to ensure your material asset files \(`.mtl`\) work properly with the new feature\. You must run the conversion script if you have authored material assets that modified the tiling, rotation, or oscillation values in the main diffuse map\. You can choose not to run the conversion script if you haven't changed material values\. However, the script converts only updated materials and is safe to run as a precaution\. You only need to run the script once per project\.

**To download the conversion script**

1. Download the conversion script [here](https://dvbcuh49skxb5.cloudfront.net/releases/1.8/1.8_IndependentTilingConvertor.py)\.

1. Save the `1.8_IndependentTilingConvertor.py` file to the `lumberyard_version\dev\Editor\Scripts\migration\1.8` directory\. You might need to create this directory\.

**To run the conversion script from a command prompt**

1. In a command line window, navigate to the Python directory for your Lumberyard installation\.

   ```
   cd lumberyard_version\dev\Tools\Python\2.7.11\windows
   ```

1. Run the conversion script by entering the following command: 

   ```
   python lumberyard_version\dev\Editor\Scripts\migration\1.8\1.8_IndependentTilingConvertor.py
   ```

1. \(Optional\) Run the script on a single project or multiple projects\.
   + To run the script on a single project, enter the following command:

     ```
     python lumberyard_version\dev\Editor\Scripts\migration\1.8\1.8_IndependentTilingConvertor.py "my_project"
     ```
   + To run the script on multiple projects at once, use commas to separate the project names and enter the following command: 

     ```
     python lumberyard_version\dev\Editor\Scripts\migration\1.8\1.8_IndependentTilingConvertor.py "my_project,my_other_project"
     ```
**Note**  
You can convert all materials in all projects within your Lumberyard build by omitting the project name\.

**To run the conversion script from Lumberyard Editor**

1. In Lumberyard Editor, choose **Tools**, **Other**, **Python Scripts**\.

1. In the **Python Scripts** window, navigate to and click **1\.8\_IndependentTilingConvertor**\.

1. Click **Execute**\.