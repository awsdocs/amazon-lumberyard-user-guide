# Boids Entity Flow Graph Nodes<a name="gems-system-gem-boids-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

## entity:*Boid Entity Type*<a name="boids-nodes-entity-name"></a>

### Inputs<a name="boids-nodes-entity-name-inputs"></a>

***Entity Name***  
Selected entity's name or label\. Displays **<Graph Entity>** if the flow graph is an [entity file](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/fg-scripts.html)\.

**Activate**  
Activates the entity\.

**Deactivate**  
Deactivates the entity\.

**AttractTo**  
Attracts the entity to a specific XYZ coordinate in the level\.  
Applies only to the birds and bald eagles entities\.

### Outputs<a name="boids-nodes-entity-name-outputs"></a>

**Activate**  
Triggers output when the entity is activated\.

**Deactivate**  
Triggers output when the entity is deactivated\.

**AttractEnd**  
Triggers output when the entity's distance is less than 5 meters from the attraction point \(**AttractTo** input\)\.  
Applies only to the birds and bald eagles entities\.

## Lua Bindings for Boids<a name="boids-lua-bindings"></a>

Individual boids have Lua\-specific behavior\. These scripts are available in `dev\Gems\Boids\Assets\Scripts\Entities\Boids`\.

The following boids functions are bound from C\+\+ to Lua:
+ CreateFlock
+ SetFlockParams
+ EnableFlock
+ SetFlockPercentEnabled
+ OnBoidHit
+ SetAttractionPoint
+ CanPickup
+ GetUsableMessage
+ OnPickup

## Console Variable for Boids<a name="boids-console-variables"></a>

The console variable `boids_enable` is defined in `dev\Gems\Boids\Code\source\ScriptBind_Boids.cpp`\. 

The `count` value for boids can be modified by the console variable `e_ObjQuality`\.