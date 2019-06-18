# Configuring the Boids Gem<a name="gems-system-gem-boids-configure"></a>

You can configure the **Entity Properties** and [https://docs.aws.amazon.com/lumberyard/latest/legacyreference/entities-params-entity-params.html](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/entities-params-entity-params.html) for the boids entity to specify such features as the number of boids to spawn per group, flocking behavior, the character model to use, and more\.

The following table lists boids entity properties and their descriptions\. As noted, certain properties appear for only specific boids\.

**Note**  
Boids spawn on terrain, not on objects placed on the terrain\.


**Boids Entity Properties**  

| Property Name | Description | 
| --- | --- | 
| Boids |  | 
| Behavior | Sets movement behavior\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-gem-boids-configure.html) | 
| Count | Number of individuals to spawn per boid group\. | 
| Invulnerable |  Sets invulnerability, where boids entities cannot by killed by anything\. When invulnerability is not set, the following can kill boids: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-gem-boids-configure.html)  | 
| Mass \(kg\) | Mass of each individual in the group\. Used when [physicalizing](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/char-phys-intro.html) the boid entity\. | 
| Model | 3D model file used for the boid representation\. You can use geometry files \(\*\.cgf, \*\.chr, \*\.skin, \*\.cdf\) for this property\. To change the model, click in the property, and then click the folder icon\. Navigate to and open the file you want to use\. The bugs boid entity has 5 Model entries for specifying 5 different models\. | 
| Flocking |  | 
| AttractDistMax |  Maximum separation distance in meters at which boids can interact with each other\. Boids do not interact with each other at distances beyond this range\.  | 
| AttractDistMin |  Minimum separation distance in meters between boids before **FactorSeparation** force affects them\.  | 
| EnableFlocking | When selected, enables flocking behavior within a group\. This means that the boids congregate or mass together\. | 
| FactorAlign | Multiplier that determines how closely boids in a group maneuver in the same direction\. | 
| FactorCohesion | Multiplier that determines how closely boids in a group congregate\. | 
| FactorSeparation | Multiplier that determines how strongly boids in a group repel one another\. Avoids crowding flock mates when closer than AttractDistMin\. | 
| FieldOfViewAngle | Viewing angle within which each boid can consider other boids flock mates\. | 
| Ground | The Ground group of properties appears only for boids entities with flight and applies only when boids are walking on the ground, which occurs only in game mode, and not in edit mode\. | 
| FactorAlign | Multiplier that determines how closely boids in a group maneuver in the same direction\. | 
| FactorCohesion | Multiplier that determines how closely boids in a group congregate\. | 
| FactorOrigin | Multiplier that determines how strongly boids in a group are attracted to their point of origin\. | 
| FactorSeparation | Multiplier that determines how strongly boids in a group repel one another\. | 
| HeightOffset | Boids vertical offset from the ground\. | 
| OnGroundIdleDurationMax | Maximum amount of time that boids idle on the ground\. | 
| OnGroundIdleDurationMin | Minimum amount of time that boids idle on the ground\. | 
| OnGroundWalkDurationMax | Maximum amount of time that boids walk on the ground\. | 
| OnGroundWalkDurationMin | Minimum amount of time that boids walk on the ground\. | 
| WalkSpeed | Speed at which boids walk on the ground when they land\. | 
| WalkToIdleDuration | Time it takes for boids to transition from walk to idle\. | 
| Movement |  | 
| FactorAvoidLand | Multiplier that determines how strongly boids in a group avoid land or water\. | 
| FactorHeight | Multiplier that determines how strongly boids in a group are kept at their original height\. | 
| FactorOrigin | Multiplier that determines how strongly boids in a group are attracted to their point of origin\. | 
| FactorTakeOff | Speed of vertical movement during takeoff\. Appears only for boids entities with flight\. | 
| FlightTime | Duration of flight before attempting to land\. Appears only for boids entities with flight\. | 
| FactorRandomAcceleration | Multiplier that determines that randomness of acceleration\. Appears only for fish boids\. | 
| HeightMax | Maximum height above land to which boids can fly\. | 
| HeightMin | Minimum height above land at which boids can fly\. | 
| LandDecelerationHeight | Height at which boids begin to decelerate when landing\. Appears only for boids entities with flight\. | 
| MaxAnimSpeed | Multiplier for maximum deviation allowed from original animation speed, for those boids with animations\. | 
| SpeedMax | Maximum speed \(meters/second\) at which boids can move\. | 
| SpeedMin | Minimum speed \(meters/second\) at which boids can move\. | 
| Options |  | 
| Activate | Activates the selected boid entity from the start of the level\. Boids can also be activated at a later stage with the activate event\. | 
| AnimationDist | Maximum distance from the camera at which animations are updated\. Appears only for boids entities with flight\. | 
| AvoidWater | Value that determines how strongly boids avoid bodies of water\. Appears only for boids that move on land\. | 
| FollowPlayer | When selected, boids flock toward current player position, which is their point of origin\. Boids stay within value set by Radius\. If boids move too far from the player, they reappear on the other side of the radius area\. | 
| NoLanding | When selected, boids with flight do not land\. | 
| ObstacleAvoidance | When selected, boids are diverted from physical obstacles\. This feature is resource\-intensive, so use it cautiously\. | 
| PickableMessage | Message that appears if a boid is able to be picked up\. Appears for all boids except fish\. | 
| PickableWhenAlive | When selected, boid can be picked up when alive\. Appears for all boids except fish\. | 
| PickableWhenDead | When selected, boid can be picked up when dead\. Appears for all boids except fish\. | 
| Radius | Maximum radius in meters that boids can move from their flock point of origin\. | 
| SpawnFromPoint | When selected, boids spawn at the boid entity position\. | 
| StartOnGround | When selected, boids spawn on the ground\. When unselected, boids spawn in the air\. | 
| VisibilityDist | Maximum camera distance in meters from which the entire flock is visible\. If the player camera's distance from the flock exceeds this value, boids are not rendered\. | 
| ParticleEffects |  | 
| EffectsScale | Scale of the particle effect to be displayed\. Appears only for frogs\. | 
| waterJumpSplash | Name of the splash particle effect to be displayed when a boid jumps into the water\. Appears only for frogs\. | 