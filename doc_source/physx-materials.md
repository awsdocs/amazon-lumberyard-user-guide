# Working with PhysX Materials<a name="physx-materials"></a>

Materials customize how an object reacts when it hits a surface and control qualities like friction and bounciness\. In Lumberyard, you specify materials for each collider\.

In Lumberyard, you store materials inside a material library that you create using the **Asset Editor**\. You can create one library with all materials for a project or separate libraries for different material types like terrain and gameplay objects\. 

**Note**  
Having one library makes it easier to see all the materials and their properties in a project\. 

**Topics**
+ [Creating a Material and Assigning it to a Collider](#physx-materials-creating-a-material-and-assigning-it-to-a-collider)
+ [Assigning Materials to the Faces of a Mesh](#physx-materials-assigning-materials-to-the-faces-of-a-mesh)
+ [**Using Materials with the Terrain**](#physx-materials-using-materials-with-the-terrain)

## Creating a Material and Assigning it to a Collider<a name="physx-materials-creating-a-material-and-assigning-it-to-a-collider"></a>

The following summary outlines the steps for working with materials in Lumberyard:

1. Create a material library\.

1. Create one or more materials for the library\.

1. Assign the library to a collider\.

1. Select a specific material from the library for the collider\.

In this topic, the example creates a material library file in the **Starter Game** project called `MaterialLibrary.physmaterial`\.

**To create a material and assign it to a collider**

1. In Lumberyard Editor, choose **Tools**, **Asset Editor**, **File**, **New**, **Physics Material**\.  
![\[Choose Physics Material in the Asset Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-1.png)

1. Navigate to the directory where you want to save the library\. The library is saved with the file extension `.physmaterial`\. The default save location is `lumberyard_version\dev\game_project\`\.

1. In the **Edit Asset** window, for **Materials**, click the plus \(**\+**\) icon to add a material \(a child element\) to the new library\.  
![\[Adding a child element to a material library.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-2.png)

1. You can specify the following options for the new material\.  
![\[Specifying option values for the material.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-3.png)  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/physx-materials.html)
**Note**  
When materials collide, the **Friction combine** and **Restitution combine** define the value of applied friction and restitution using the following order\.  
**Average**
**Minimum**
**Multiply**
**Maximum**

1. Save your changes to the asset\.

1. In the Lumberyard Editor viewport, [create](creating-entity.md) or select the entity that will use the material that you created\.

1. In the **Entity Inspector**, click **Add Component**, and then add the **PhysX Collider** component to the entity\.

1. In the **PhysX Collider** component, next to **Material Library**, click the **Browse** \(**\.\.\.**\) icon\.  
![\[Choose the ... icon to navigate to a material library.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-4.png)

1. In the **Pick Physics Material** dialog box, choose the library that you created, and then click **OK**\.  
![\[Choose the material library that you created.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-5.png)

1. In the **PhysX Collider** component, for **Entire Object**, choose the material that you created\.  
![\[Choose a material that you created.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-6.png)

The material that you created is now assigned to the collider that you chose\.

## Assigning Materials to the Faces of a Mesh<a name="physx-materials-assigning-materials-to-the-faces-of-a-mesh"></a>

You can assign more than one material to faces of a single mesh\. To mark up faces on the mesh, you can use placeholder rendering materials in Maya\. This strategy offers the following advantages:
+ Familiar tools to paint materials on a mesh\.
+ Simple textures for visualization\.

The following sample walkthrough exports a house as a single mesh and assigns different materials for the windows, porch, walls, and door\.

**To assign materials to the faces of a mesh**

1. In Maya Hypershade, create four placeholder materials and give them the following names:
   + **door**
   + **walls**
   + **porch\_concrete**
   + **windows\_glass**

   Lumberyard uses a soft naming convention for materials\. For example, Lumberyard automatically creates a **road** slot for Maya material called **road\_dirt** and automatically attempts to assign the **dirt** material from the selected material library\. For more information, see [FBX Soft Naming Conventions](char-fbx-importer-soft-naming.md)\.
**Note**  
Lumberyard recognizes names without an underscore \(\_\) as slot names\.

1. Paint the materials on the mesh faces and export the result as an `.fbx` file\.

1. In Lumberyard Editor, [create an entity](creating-entity.md)\.

1. In the **Entity Inspector**, add a **[PhysX Collider](component-physx-collider.md)** component to the entity\.

1. In the **PhysX Collider** component, for **Shape**, choose **PhysicsAsset**\.

1. [Export](physx-export-physx-mesh-asset.md) a `.pxmesh` file as a static object\. To make the mesh a static object, ensure that the **Export Mesh As Convex** check box in the ****FBX Settings**** tool is cleared\.  
![\[Clear the Export Mesh as Convex option in the Fbx Settings tool.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-7.png)

1. Select the generated `.pxmesh` file for the collision\.

1. Follow the steps in [Creating a Material and Assigning it to a Collider](#physx-materials-creating-a-material-and-assigning-it-to-a-collider) to assign a physics material library and materials to the collider\.  
![\[Assigning materials to imported material slots in the PhysX Collider component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-8.png)

   The **Material** section now shows the **walls**, **windows**, **door**, and **porch** slots that you exported from the `.fbx` file and the materials that you assigned to them\.

## **Using Materials with the Terrain**<a name="physx-materials-using-materials-with-the-terrain"></a>

By default, terrain is assigned with the default material\. Use the **[Terrain Texture Layers](terrain-texture-layers-intro.md)** editor to assign materials to different surface types\.

![\[Surface ID and Material Library properties in the Terrain Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/physx-materials-9.png)

**Note**  
For terrain materials to work properly, you must have a **[PhysX Terrain](component-physx-terrain.md)** component in your scene\. If you modify material properties on layers without a **PhysX Terrain** component in a scene, a warning appears in the console window, and your changes are not saved\.
To ensure the engine generates a unique surface ID that can be later assigned with the physics material, you must change material on the layer\. If multiple layers share the same surface ID, they can be assigned only one physics material\.