# Navigation Area<a name="component-nav-area"></a>


****  

|  | 
| --- |
| This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

The **Navigation Area** component defines the features of a navigable area or volume for use by the AI System\. You use this component with the **[Polygon Prism Shape](component-polygon-prism.md)** component, which defines the volume of the navigation area\.

**Note**  
When you add a **Navigation Area** component, you must also add the **Polygon Prism Shape** component\. 

For instructions on how to adjust the **Polygon Prism Shape** component, see [Polygon Prism Shape](component-polygon-prism.md)\.

When you create a **Navigation Area**, all areas that are traversable by the specified AI [**Agent Type**](#component-nav-area-properties) show as blue when you [render the navigation mesh](#render-navigation-mesh)\. Any areas that are not traversable render as blank areas, such as deep pits and steep slopes\. Exclusion areas and areas around static objects also render as blank areas\. Even if your navigation area is divided into separate pieces by static objects, terrain features, and exclusion areas, each traversable area renders blue\.

![\[Navigation Area component properties.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area.png)

You can use a **[Navigation Seed](component-nav-seed.md)** component to fine\-tune AI accessibility\.

**To add a Navigation Area**

1. In the Viewport, near where you want to create your navigation area, right\-click and choose **Create entity**\.

1. With your new entity selected in the **Entity Outliner**, [add](component-working-adding.md) the **Navigation Area** component to it\.  
![\[Navigation Area component properties.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-1.png)

1. In the **Navigation Area** component, next to **Agent Types**, click **\+**\.

   Next to **\[0\]**, select **MediumSizedCharacters**\. This property defines the [types of agents](#component-nav-area-properties) that can navigate in this area\.

1. Add the **Polygon Prism** component\. [Adjust the size and shape](component-polygon-prism.md#working-with-polygon-prism-components) of the **Polygon Prism**\. Ensure that your terrain and objects intersect with the volume of the polygon prism\. [Adjust the height](component-polygon-prism.md#component-polygon-prism-height-adjustment) if necessary\.

   If your polygon prism hovers above your terrain and does not fully intersect with it, the navigation system does not produce the appropriate traversable areas\. The following examples show a navigation area that is too high above the terrain \(1\), and a navigation area appropriately situated on the terrain \(2\)\. If your navigation area is too high, use the [move](lumberyard-editor-toolbars.md#lumberyard-editor-toolbars-editmode) tool to lower the Z \(up and down\) position of the entity\.  
![\[Enable Show Navigation Areas and View Agent Type in Lumberyard Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-1.1.png)

**To view the generated Navigation Area mesh**

1. In Lumberyard Editor, choose **Game**, **AI**, **Show Navigation Areas**\.

1. In Lumberyard Editor, choose **Game**, **AI**, **View Agent Type**, and then enable the agent type that you want to display\.  
![\[Enable Show Navigation Areas and View Agent Type in Lumberyard Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-3.png)

1. In Lumberyard Editor, choose **Game**, **AI**, **Generate All AI**\.

   A navigation mesh is generated showing traversable areas in blue\. To enable continuous update, which shows changes in the navigation mesh as you modify the terrain or area, select **Game**, **AI**, **Continuous Update**\.

**Topics**
+ [Navigation Area Component Properties](#component-nav-area-properties)
+ [Navigating Around Static Objects](#component-nav-area-static-entities)
+ [Creating Navigation Mesh Exclusion Areas](#component-nav-area-exclusion)
+ [EBus Request Bus Interface](#component-nav-area-ebus)

## Navigation Area Component Properties<a name="component-nav-area-properties"></a>

The **Navigation Area** component has the following properties:<a name="component-nav-area-properties-agent-types"></a>

**Agent Types**  
Specifies the types of AI that can traverse this navigation area\. These agent types are defined in `lumberyard_version\dev\your_project_name\Scripts\AI\Navigation.xml`\. To specify multiple agent types for this area, click the **\+** icon\.   
You use this property to restrict which agents can navigate within that area\. For example, you can allow characters to navigate within a narrow corridor but restrict vehicles\.  
To define an agent type on your AI, see the [Navigation](component-navigation.md) component\.

**Exclusion**  
When selected, creates a subtractive navigation area\. This creates a cutout within an existing navigation mesh\. For more information, see [Creating Navigation Mesh Exclusion Areas](#component-nav-area-exclusion)\.

![\[Enable Show Navigation Areas and View Agent Type in Lumberyard Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-3.png)

## Navigating Around Static Objects<a name="component-nav-area-static-entities"></a>

When Lumberyard creates the navigation mesh, it can automatically exclude areas that should not be traversable, such as a large boulder or tree trunk\. To ensure that these areas are correctly detected by the navigation system, you must specify its **Transform** component as static\. 

**To mark an entity as static**

1. In the **Entity Outliner**, select the entity\. This can be a tree, boulder, building, or any object that you don't want the AI to walk through\.

1. In the **[Transform](component-transform.md)** component, select the **Static** property\.

   The following example shows a navigation mesh around a boulder when the **Static** property is not selected\.

![\[Navigation mesh goes through the boulder because Static is not selected on the boulder's Transform component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-4.png)

The following example shows the same navigation mesh, but with the **Static** property selected on the boulder\.

![\[Navigation mesh creates an exclusion area around the boulder, because Static is selected on the boulder's Transform component\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-5.png)

## Creating Navigation Mesh Exclusion Areas<a name="component-nav-area-exclusion"></a>

You can use the **Navigation Area** component to manually create areas to exclude from the navigation mesh\. This means that the AI agents cannot traverse these areas\. To do this, you create a navigation area and select the **Exclusion** property, as shown in the following image\.

![\[Select the Exclusion property to create a navigation area that subtracts from the navigation mesh\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-8.png)

The following example shows a navigation mesh \(1\) and the same navigation mesh with an exclusion area \(2\)\.

![\[Navigation Area component, when marked as an exclusion, subtracts or creates a hole or non-traversable area in the navigation mesh\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-nav-area-6.png)

**To create an exclusion area**

1. If you have not already, you must first [create a navigation area](#create-navigation-area) that is not an exclusion area\.

1. Create an entity, and add to it the **Navigation Area** and **Polygon Prism Shape** components\.

1. In the **Navigation Area** component, select the **Exclusion** property\.

1. In the **Viewport**, place the exclusion area within the navigation mesh\.

1. Shape the polygon to the preferred shape for the exclusion area\.

## EBus Request Bus Interface<a name="component-nav-area-ebus"></a>

Use the following request function with the `NavigationAreaRequestBus` EBus interface to communicate with other components of your game\. 

For more information about using the event bus \(EBus\) interface, see [Working with the Event Bus \(EBus\) System](ebus-intro.md)

### RefreshArea<a name="component-nav-area-ebus-refresharea"></a>

You can use the [PolygonPrismShapeComponentRequestBus](component-polygon-prism.md#component-polygon-prism-ebus-request) to modify the polygon prism area by adding, removing, and updating its vertex positions\. Use `RefreshArea` to update the navigation area after making changes to the area\.

**Parameters**  
None

**None**  
`AZ::ConstPolygonPrismPtr`

**Scriptable**  
No

**Note**  
The Navigation Area component depends on the Polygon Prism component, which also uses `VertexContainer` functions\. For more information, see [Vertex Containers](component-vertex-container.md)\.