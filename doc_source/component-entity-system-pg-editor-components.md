# Editor Components<a name="component-entity-system-pg-editor-components"></a>

Some components in Lumberyard have separate `editor` and `runtime` versions\. The editor version is active in the editor\. The runtime version is used for running the level in game or in the editor by pressing **Ctrl\+G** or clicking **AI/Physics** below the viewport\. Lumberyard uses editor components to maintain a clean separation between tools\-specific code and data on one hand, and leaner runtime component data on the other\. In general, runtime game components do not require editor counterparts\. Components rarely need to be fully active at edit time\. The light and mesh components are exceptions because they must behave the same at edit time as at run time\.

`EditContext` reflection is fully supported in runtime components\. Edit time is the only time when editor components are active\. At run time, when Lumberyard processes a level or dynamic slice, it uses the runtime equivalents of editor components\. Using the `EditContext` from a runtime component is usually sufficient to provide a rich editing experience\.

**Important**  
Editor components are not required\. An editor component is necessary only if one of the following is true:  
Your component must be fully active at edit time\. Edit time refers to standard editing mode; runtime components are used for the **AI/Physics** mode and gameplay \(**Ctrl\+G**\)\.
You must add special tools functionality to your component that requires that you compile only into your editor binaries\.
Your component provides functionality only in the editor and does not export a runtime component \(for example, if your component manages selection logic\)\.

## Sample Editor Component<a name="component-entity-system-pg-editor-components-sample"></a>

The following code shows a sample editor component\.

```
class MyEditorComponent 
      : public AzToolsFramework::Components::EditorComponentBase
      , private AzFramework::EntityDebugDisplayEventBus::Handler
{
public:
      AZ_EDITOR_COMPONENT(MyEditorComponent, "{5034A7F3-63DB-4298-83AA-915AB23EFEA0}");
 
      // AZ::Component interface implementation.
      void Init() override            {}
      void Activate() override      {}
      void Deactivate() override      {}

    
      // AzFramework::EntityDebugDisplayEventBus::Handler.
      void DisplayEntity(bool& handled) override;
    
      // Required Reflect function.
      static void Reflect(AZ::ReflectContext* context);
 
      // Optional functions for defining provided and dependent services.
      static void GetProvidedServices(AZ::ComponentDescriptor::DependencyArrayType& provided);
      static void GetDependentServices(AZ::ComponentDescriptor::DependencyArrayType& dependent);
      static void GetRequiredServices(AZ::ComponentDescriptor::DependencyArrayType& required);
      static void GetIncompatibleServices(AZ::ComponentDescriptor::DependencyArrayType& incompatible);
      
      
      void BuildGameEntity(AZ::Entity* gameEntity) override;
      
};
```

## Editor Component and Runtime Component Differences<a name="component-entity-system-pg-editor-components-editor-runtime-differences"></a>

The code for editor components is similar to the code for runtime components\. The following sections list the key differences\. It is safe to assume that editor component code is the same as it is for runtime component code other than the differences listed\. For more information, see [Creating a Component](component-entity-system-create-component.md)\.

### Base Classes<a name="component-entity-system-pg-editor-components-base-classes"></a>

All editor components include the `AzToolsFramework::Components::EditorComponentBase` class somewhere in their inheritance ancestry\. If a component must display edit\-time visualization, it must be a handler on the `AzFramework::EntityDebugDisplayEventBus::Handler` bus, as in the following example\.

```
class MyComponent 
      : public AzToolsFramework::Components::EditorComponentBase
      , private AzFramework::EntityDebugDisplayEventBus::Handler
```

### Macro<a name="component-entity-system-pg-editor-components-macro"></a>

Every editor component must specify the `AZ_EDITOR_COMPONENT` macro within its class definition\. The macro takes two arguments:

1. The component type name\.

1. A unique UUID\. You may use any UUID generator to produce the value\. Visual Studio provides this functionality through **Tools**, **Create GUID**\. Use the **Registry Format** setting, and then copy and paste the value that is generated\.

A sample `AZ_EDITOR_COMPONENT` macro follows\.

```
AZ_EDITOR_COMPONENT(MyEditorComponent, "{5034A7F3-63DB-4298-83AA-915AB23EFEA0}");
```

**Note**  
Some older editor components specify `AzToolsFramework::Components::EditorComponentBase` as the base class but use the `AZ_COMPONENT` instead of the `AZ_EDITOR_COMPONENT` macro, as in the following example\.  

```
AZ_COMPONENT(EditorMannequinComponent, "{C5E08FE6-E1FC-4080-A053-2C65A667FE82}", AzToolsFramework::Components::EditorComponentBase);
```

### The DisplayEntity Method<a name="component-entity-system-pg-editor-components-displayentity"></a>

To render special visualizations in the editor, implement the `DisplayEntity` method of the `AzFramework::EntityDebugDisplayEventBus` interface\. Use this location for custom primitive edit\-time visualization code\.

```
// AzFramework::EntityDebugDisplayEventBus::Handler
void DisplayEntity(bool& handled) override;
```

### The BuildGameEntity Method<a name="component-entity-system-pg-editor-components-buildgameentity"></a>

The `BuildGameEntity` method facilitates the translation of an editor component into a runtime component\. Its syntax is as follows\.

```
void BuildGameEntity(AZ::Entity* gameEntity) override;
```

A typical implementation of the `BuildGameEntity` method performs the following actions:

1. Create a runtime component based on the editor component of the specified `gameEntity`\.

1. Copy the configuration data from the editor component into the runtime component\.

1. Add the runtime component to the `gameEntity` that was specified\.

At this point, the runtime component serializes the `gameEntity` and reloads it to create a new, clean version of the runtime entities\.

### The Transform Component Example<a name="component-entity-system-pg-editor-components-transform-component-example"></a>

The `TransformComponent` is a good example of how editor and runtime components can differ\. In the runtime component, values are stored in a fully composed `AZ::Transform`\. In the editor component, values are stored in decomposed format\. Position, rotation, and scale values are stored separately, and rotation is represented as Euler angles\. This difference in format enables the editor component to provide user\-friendly display and storage while providing optimal storage in the runtime component\.