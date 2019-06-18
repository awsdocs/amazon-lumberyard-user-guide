# PhysX Collider<a name="component-physx-collider"></a>

The **PhysX Collider** component provides a shape to the physics object\. How the object moves or not depends on the **[PhysX Rigid Body Physics](component-physx-rigid-body-physics.md)** component\.
+ If the entity has the **PhysX Collider** component only, Lumberyard treats the entity as a static collider that doesn't move\. This can be useful for creating game objects such as a wall or mountain\.
+ If the entity also has the **PhysX Rigid Body Physics** component, Lumberyard treats the entity as a dynamic collider\. Dynamic colliders mean that the entity can move\. 

You can specify how the entity behaves or interacts with other entities in the **PhysX Collider** properties\. You can also attach multiple **PhysX Collider** components to an entity, so that you can define different mesh colliders\.

The **PhysX Collider** component requires the [PhysX](gems-system-gem-physx.md) gem\.

For more information, see [Simulating Physics Behavior with the PhysX System](physx-intro.md)\.

**Topics**
+ [PhysX Collider Properties](#component-physx-collider-properties)
+ [Creating a Static PhysX Entity](#creating-a-static-physx-entity)
+ [Primitive Colliders](#primitive-colliders)
+ [Creating Mesh Colliders](#creating-mesh-colliders)
+ [Colliders as Triggers](#colliders-as-triggers)
+ [Exporting a PxMesh Asset](physx-export-physx-mesh-asset.md)

## PhysX Collider Properties<a name="component-physx-collider-properties"></a>

![\[PhysX Collider component properties.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-physx-collider-1.png)

The **PhysX Collider** component has the following properties\.


****  

| Property | Description | 
| --- | --- | 
|  **Collision Layer**  |  Collision layer on which this collision exists\. For more information, see [Collision Layers](physx-configuration-collision-layers.md)\.  | 
|  **Collides With**  |  Layers in which this collider will intersect\. For more information, see [Collision Groups](physx-configuration-collision-groups.md)\.  | 
|  **Draw Collider**  |  Renders the collider in the viewport\. Set this property so that you can view how your entities interact\.  Enabled by default\.   | 
|  **Trigger**  |  Turns the collider into a trigger\.  | 
|  **Offset**  |  Local offset of the collider relative to the entity\.  | 
|  **Rotation**  |  Local rotation of the collider relative to the entity\.  | 
|  **Material Library**  |  Material assigned to the collider\.  | 
|  **Shape**  |  Shape of the collider\. You can specify the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/component-physx-collider.html) For more information, see [Primitive Colliders](#primitive-colliders)\. If you want to use a custom collider shape, you can specify the following; [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/component-physx-collider.html) For more information, see [Creating Mesh Colliders](#creating-mesh-colliders)\.  | 
|  **Radius** \(Sphere only\)  |  Radius of the sphere collider\. Sphere takes the largest value in the **Scale** property in the **[Transform](component-transform.md)** component and multiplies it with the **Radius**\.  | 
|  **Dimensions ** \(Box only\)  |  Dimensions of the box collider\.  | 
|  **Height ** \(Capsule only\)  |  Total height of the capsule collider\. If you set a value that is less than twice the **Radius**, the **Height** defaults to a value that is twice the **Radius**\. For example, if the **Radius** is `5` and you set a **Height** at `7`, this value changes to `10`\.  | 
|  **Radius ** \(Capsule only\)  |  Radius of the capsule collider\. You can't specify a value that is greater than half the value for **Height**\. For example, if the **Height** is `10`, the radius can be a maximum of `5`\.  | 
|  **Asset Scale ** \(PhysicsAsset only\)  |  Scale of the asset collider\.  You can use this property to modify the physics collider shape independent of the entity\.   | 
|  **PxMesh ** \(PhysicsAsset only\)  |  The pxmesh asset assigned to the collider \(convex mesh only\)\. For more information, see [Exporting a PxMesh Asset](physx-export-physx-mesh-asset.md)\.  | 

## Creating a Static PhysX Entity<a name="creating-a-static-physx-entity"></a>

A PhysX entity that is static can interact with other entities, but doesn't move\.

**To create a static PhysX entity**

1. Create an entity\. For more information, see [Creating an Entity](creating-entity.md)\.

1. In the **Entity Inspector**, choose **Add Component** and then select a **[Mesh](component-static-mesh.md)** component\.

1. For **Mesh asset**, select the mesh asset so that your entity is visible, such as a `tree_08.cgf`\.

1. Add the **PhysX Collider** component to the entity\.

1. Press **Ctrl\+G** to enter gameplay mode\. Your entity is static and doesn't move\.  
**Example**  

   The entity has a **PhysX Collider** component\. Because the entity doesn't have a **PhysX Rigid Body Physics** component, this entity is static\.  
![\[PhysX Collider component example entity that is static.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-physx-collider-3.png)
**Note**  
For the **[Transform](component-transform.md)** component, leave the **Static** property enabled\. This ensures that the mesh doesn't move\.
If you want your entity to move, add the **PhysX Rigid Body Physics** component\. 

## Primitive Colliders<a name="primitive-colliders"></a>

When you add the **PhysX Collider** component to an entity, you can specify the following basic collider shapes:
+ **Box**
+ **Sphere**
+ **Capsule**

These shapes are primitive colliders because there isn't an underlying mesh that represents the shape\. They require less performance than other types of colliders and should be used when possible\.

## Creating Mesh Colliders<a name="creating-mesh-colliders"></a>

The fourth type of collider is an asset collider\. You can specify an asset collider when the accuracy of the collider must be precise\. For example, you might add an asset collider when you want to specify a custom shape for your entity\. To do this, use a mesh to set up the collider geometry and assign a pxmesh asset to the component\. It is common to use mesh colliders for static geometry in the scene\.

**Note**  
If you want to define your mesh collider to have different properties, you can do the following:  
Use a third\-party tool such as Maya to define your mesh collider and then import the pxmesh asset into Lumberyard Editor\.
Attach multiple **PhysX Collider** components to the entity, and then specify different pxmesh assets and properties for each component\.

**To create a mesh collider**

1. Create an entity\. For more information, see [Creating an Entity](creating-entity.md)\.

1. In the **Entity Inspector**, choose **Add Component** and then select a **[Mesh](component-static-mesh.md)** component\.

1. For **Mesh asset**, select the mesh asset so that your entity is visible\.

1. To make the entity dynamic, add the **PhysX Rigid Body Physics** component\. 

1. Add the **PhysX Collider** component to the entity\.

1. In the **PhysX Collider** properties, for **Shape**, select **PhysicsAsset**\.

1. For **PxMesh**, specify the pxmesh asset\. Your entity has a custom shape and collider geometry\.  
![\[PhysX Collider component properties for asset and pxmesh.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-physx-collider-2.png)
**Note**  
To generate `.pxmesh` files for your game project, see [Exporting a PxMesh Asset](physx-export-physx-mesh-asset.md)\.   
**Example**  

   Instead of a primitive shape, the entity has a pxmesh asset specified for the **PhysX Collider** component\.  
![\[PhysX Collider component with a custom pxmesh asset to create a custom collider shape.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-physx-collider-4.png)
**Note**  
Only convex meshes can be used for dynamic colliders\. If you assign a non\-convex mesh, the collider won't work\.

## Colliders as Triggers<a name="colliders-as-triggers"></a>

Colliders can also operate as triggers, allowing them to perform overlap tests that require less processing\. Colliders marked as triggers will not have forces applied when they intersect with another collider\. Notifications appear when a trigger overlaps with another collider\. This is useful for detecting when something enters a certain area or when two objects overlap\.

**Note**  
Because triggers don't perform contact resolution, the contact points between a trigger and another collider aren't available\.