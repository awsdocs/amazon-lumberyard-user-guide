# Object Shadows<a name="rendering-graphics-shadows-object"></a>

With object shadows, you can assign custom shadow maps to selected objects, resulting in increased shadow quality due to higher world space shadow texel \(texture element\) density and reduced depth range\.

The drawbacks of using object shadows are increased memory consumption of the additional shadow maps and increased shadow filtering cost\.

Object shadows only affect sun shadows\. For performance reasons they are not sampled on forward geometry such as particles, hair, and eyes\.

## Using Flow Graph<a name="rendering-graphics-shadows-object-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can use the **Environment:PerEntityShadows** flow graph node and assign the target entity to the **Entity** slot\. The **Trigger** input applies the settings to Lumberyard\.

Because this node is stateless with respect to the entity, you can add multiple **Environment:PerEntityShadows** nodes for the same entity\. The last one to be triggered will be in effect\. 

Use the following node inputs to tweak the shadow appearance:
+ **ConstBias/SlopeBias** – Reduces avoid self\-shadowing artifacts\.
+ **Jittering** – Filters kernel size, which directly affects shadow softness\.
+ **BBoxScale** – Scale factor for the bounding box of the selected entity\. Can be useful in case the bounding box is too small or too large\.
+ **ShadowMapSize** – Size of the custom shadow map, which is automatically rounded to the next power of two\.

## Using I3DEngine<a name="rendering-graphics-shadows-object-i3dengine"></a>

The following I3DEngine interface functions can be called from anywhere in game code\. The function parameters are equivalent to the parameters for the **Environment:PerEntityShadows** Flow Graph node\. 
+ **AddPerObjectShadow** – Adds an object shadow\.
+ **RemovePerObjectShadow** – Removes an object shadow\.
+ **GetPerObjectShadow** – Retrieves object shadow settings for a given `RenderNode`\. Do not overwrite the `RenderNode` pointer\. Instead use `AddPerObjectShadow\RemovePerObjectShadow`\.
+ **ShadowMapSize**: Size of the custom shadow map, which is automatically rounded to the next power of two\.

## Console Variables<a name="rendering-graphics-shadows-object-cvars"></a>

You can use the **e\_ShadowsPerObject** console variable with object shadows\. With this variable, 0 = 0ff, 1 = on, and \-1 = don't draw object shadows\.