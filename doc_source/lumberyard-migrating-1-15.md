# Lumberyard 1\.15<a name="lumberyard-migrating-1-15"></a>

Previously, Lumberyard animation files \(`.actor`, `.motion`, `.motionset`, `.animgraph`\) were binary files\. Lumberyard 1\.15 introduces a text\-based file format for motion sets \(`.motionset`\) and animation graphs \(`.animgraph`\)\. This allows you to edit and merge files that multiple people have simultaneously worked on\.

![\[Example of text and binary animation files in the Amazon Lumberyard Animation Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/animation-editor-text-based-file-format.png)

## Making Batch Edits<a name="lumberyard-migrating-1-15-making-batch-edits-animation-editor-text-files"></a>

You can make batch edits to your text file\. For example, you can open a `.motionset` file and batch rename or change all transition times to a specific value for multiple transitions\.

**To make batch edits**

1. In your preferred text editor, open the text file\.

1. Make your batch edits\.

1. Save the text file\.

## Resolving Conflicts<a name="lumberyard-migrating-1-15-resolving-conflicts-animation-editor-text-files"></a>

If you use a source control solution, such as Perforce or Alienbrain, we recommend that multiple people work on different parts of the motion set or animation graph file\. For example, two people can change different properties of the same node\.

This prevents merge conflicts from the following situations:
+ Two people rename the same node in an animation graph\.
+ Two people change the same property in a node\.
+ One person deletes a node while another person changes the property of that node\.

To resolve merge conflicts, follow the process for your source control solution\.

## Migrating Custom Nodes to use the Lumberyard Reflection System<a name="lumberyard-migrating-1-15-migrating-custom-animation-nodes"></a>

Lumberyard 1\.15 introduces the following changes for animation graph objects:
+ Animation graphs are now stored in a text\-based file format that allows you to easily edit and merge files\. Multiple people can also simultaneously collaborate on animation graphs and motion sets\.
+ You can now serialize animation graphs as text\-based XML files or binary files\. Animation graphs will also support other file formats that are added to the Lumberyard serialization framework\.
+ The `RegisterPorts()` function has been removed\. You can now specify input and output ports in the constructor\.
+ You can now use the `ChangeNotify` callback in the edit context to update data that changes, as well as reflected data, such as instanced data\. Previously, you updated data in the `OnUpdateAttributes()` function\.

  For example, an animation graph node may have a string stored for a joint\. If the string changes and you don't want to store the string at runtime, an integer is stored that holds the joint index\. You can then access the joint directly, rather than searching for it by name\. Whenever the joint is selected, the joint index integer must be updated\. This is where the `ChangeNotify` callback is useful\.
+ When you register your custom node with `EmotionFXAnimation::EMotionFXRequestBus::Events::RegisterAnimGraphObjectType`, the custom node is added to a list that is used to show custom nodes in the UI\.

As a result of these changes, you must migrate any custom EMotion FX objects or nodes that you created in Lumberyard 1\.14 or earlier, if you want to use them for game projects in Lumberyard 1\.15\.

**To migrate custom nodes**

1. In Visual Studio or your preferred code editor, open the header file for your custom node\.

1. In the custom node class interface, delete the MCORE memory object category\.

1. Add your custom node to the runtime type information \(RTTI\) system by adding the following:

   ```
   AZ_RTTI(MyCustomNode, "{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX}", AnimGraphNode)
   ```

1. Specify the allocator by doing the following:
   + In the header file, add `AZ_CLASS_ALLOCATOR_DECL` to the class definition\.
   + In the source file, add `AZ_CLASS_ALLOCATOR_IMPL(MyCustomNode, AnimGraphAllocator, 0)`\.

1. Move the content in the `RegisterPorts()` function to the constructor\.

1. Delete the following functions:
   + `Clone()`
   + `GetTypeString()`
   + `RegisterAttributes()`

1. Change attributes to class members\. For example, `AttributeFloat` becomes a float class member, and a combo box becomes an enum value\.

1. Replace `GetAttributeX()` calls with the class members, which now store the values\. This ensures the `Update()`, `PostUpdate()`, and `Output()` functions compile after you replace the attributes with class members\.

1. Add a `Reflect()` function, and then add your class members to the serialize and edit context attributes\. This reflects the new node, stores the settings in the animation graph files, and allows you to see the UI elements\.

1. Use a `ChangeNotify` callback in the edit context attribute for data that you previously updated in the `OnUpdateAttributes()` function\.

1. Call the `Reflect()` function for your custom node\.

1. Recompile your code\. For more information, see [Building Your Game Project](building-your-lumberyard-game-project.md)\.

## Migrating Custom Attributes<a name="lumberyard-migrating-1-15-migrating-custom-attributes"></a>

If you created custom attributes for your custom nodes, you must do the following:
+ Move the custom attribute to a member in your custom node\.
+ Port the custom attribute by doing one of the following:
  + Keep your custom data in a class and remove all attribute\-related functionality\. You can then reflect the custom data class and add a member to your node\.
  + Move the custom data from the attribute to the custom node\. Reflect the data and the custom node\.
+ Use a custom property handler to change the new property in the UI\.

No changes are needed if you only used the provided attributes, such as float \(spinner, slider\), int \(spinner slider, combo box\), bool \(check box\), node names, or motion pickers\.

**To add your custom node to the backward compatible file loader**

1. Add your custom node type to the node type mapping: `newTypeIdByOldNodeTypeId`, line 73\. This tells the file loader how to translate the old type IDs to the new UUID\-based types\.

1. In the node attributes, create a `LegacyAnimGraphNodeParser::ParseAnimGraphNode<MyCustomNodeType>` function\. For an example, see the `BlendTreeAccumTransformNode`, line 3555\.
**Note**  
You must parse custom attributes in this function\.

1. Add your custom node type to the check in `LegacyAnimGraphNodeParser::ParseAnimGraphNodeChunk(...)`, line 2689\.

1. Call the parse function `LegacyAnimGraphNodeParser::ParseAnimGraphNode<MyCustomNodeType>(...)` that you created in step 2\.