# AI Navigation<a name="ai-nav-intro"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

Lumberyard has a robust set of tools and methods for moving AI agents around – from simple point\-to\-point navigation to complex sets of scripted navigation behaviors\.

AI agents come in different sizes and with different physical properties that impact how they navigate through a game level\. AI agent types that can navigate include animate entities such as humans and aliens, and vehicles such as cars, boats, and aircraft\. 

Each AI has its own navigation mesh that defines the 3D volume where it can move around in\. This navigation mesh is called the Multi\-Layer Navigation Mesh \(MNM\), and consists of 3D navigation areas, exclusion areas where it cannot move in, and navigation seed points\. 

You define where and how an AI agent moves around in the navigation mesh using Flow Graph logic\. Flow Graph allows you to quickly create complex scripted movements and animations for AI agents as they navigate throughout the area\.

AI agents can also move along defined paths between navigation meshes \- this is called off\-mesh navigation\.

**Topics**
+ [Multi\-Layer Navigation Mesh \(MNM\)](ai-nav-mesh.md)
+ [Creating Navigation Areas](ai-nav-areas.md)
+ [Selecting an AI Navigation Type](ai-nav-agent-types.md)
+ [Setting Navigation Exclusion Areas](ai-nav-areas-exclusion.md)
+ [Adding Navigation Seed Points](ai-nav-seed-points.md)
+ [Using Flow Graph for AI Navigation](ai-nav-fg.md)
+ [Regenerating the Navigation Mesh](ai-nav-mesh-regen.md)
+ [Off\-Mesh AI Navigation](ai-nav-off_mesh_intro.md)
+ [Tutorial: Basic AI Navigation](ai-nav-tutorial.md)
+ [Debugging AI Navigation](ai-nav-debug.md)
+ [Navigation Q & A](ai-navigation.md)