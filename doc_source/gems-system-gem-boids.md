# Boids Gem<a name="gems-system-gem-boids"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

The Boids Gem provides entities that simulate animated animals that produce sound, exhibit group behavior, and avoid obstacles\. Their complex behavior arises from the interaction of an individual agent boid with other boids and their environment\.

A boids entity is a group of animals\. You can control such aspects as the total number of boids, their mass, flocking behavior, speed, interaction with the player, and more\. All boids entities exhibit by default a combination of basic motion, player avoidance, and flocking behavior\.

The boids entity can also be affected by other entities; for example, a rain entity placed in the same scene with a turtles entity results in wet turtles\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems-system-gem-boids-intro.png)

**Topics**
+ [Configuring the Boids Gem](gems-system-gem-boids-configure.md)
+ [Boids Entity Flow Graph Nodes](gems-system-gem-boids-fg.md)

**To place Boids entities**

1. In the **Rollup Bar**, on the **Objects** tab, click **Entity**\.

1. Expand **Boids**\.

1. Drag one of the boids entities into your level in the **Perspective** viewport\.