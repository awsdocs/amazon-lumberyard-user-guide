# Tornadoes Gem<a name="gems-system-gem-tornado"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 


****  

|  | 
| --- |
| This gem is deprecated and will be removed in a future release\. | 

The Tornadoes Gem creates realistic tornado effects in your levels\.

You can place your tornado and customize it to your level by modifying such properties as its height, funnel effect, radius, spin impulse, and so on\. To enable the Tornadoes Gem in your project, see [Using Gems to Add Modular Features and Assets](gems-system-gems.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems-system-gem-tornado.png)

**To add a tornado to your level**

1. In the **Rollup Bar**, click **Entity**\.

1. Under **Browser**, expand **Environment**\.

1. Drag the **Tornado** entity into your scene\.

## Configuring Tornadoes<a name="gems-system-gem-tornado-configuring"></a>

You can configure the properties for the tornado entity to set properties for attraction impulse, spin speed affecting close objects, wander speed, and more\. You can also set what type of material is inside the tornado\.

**To configure the tornado parameters and properties**

1. Select the tornado entity you want to configure\.

1. Under [https://docs.aws.amazon.com/lumberyard/latest/legacyreference/entities-params-entity-params.html](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/entities-params-entity-params.html) and **Entity Properties**, select or clear check boxes for the preferred effects\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems-system-gem-tornado-props.png)


**Tornado Entity Properties**  

| Properties | Description | 
| --- | --- | 
| AttractionImpulse | Specifies how strongly the tornado attracts objects\. | 
| CloudHeight | Sets the height of the clouds above the tornado | 
| FunnelEffect | Sets the specified particle effect defined in one of the tornado\.xml files as explained in [Customizing a Tornado Preset](#gems-system-gem-tornado-customizing)\. | 
| Radius | Sets the area that the tornado influences | 
| SpinImpulse | Sets the spin speed that affects objects close to the tornado | 
| UpImpulse | Sets the speed of upward pull that affects objects close to the tornado | 
| WanderSpeed | Sets the speed at which the tornado moves | 

## Customizing a Tornado Preset<a name="gems-system-gem-tornado-customizing"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can customize your tornado entity using the presets in the `tornado.xml` file\.

**To use or customize a tornado preset**

1. In a text editor, open `\dev\Gems\Tornadoes\Assets\libs\Particles\tornado.xml ` in the Lumberyard root directory \(`lumberyard_version\dev`\)\.

1. Choose one of the existing presets from the `tornado.xml` file \(follows **Arc name** in the example\) and, in Lumberyard Editor, under **Entity Properties**, enter your chosen **Arc name** into the **ArcPreset** field\.

   For example, enter **ExtendedArc** or **KickSparks**, which are existing names of presets as shown in the following `lightningarceffects.xml` file\. This sample shows only the partial contents; open the file on your computer to view the full contents of the file\.

   Do one of the following:
   + Copy one of the existing presets \(see example of a preset below\)\.
   + Create your own new preset in the file and copy it\.

1. In the **Rollup Bar**, on the **Objects** tab, click **Entity**\. Under **Entity Properties**, click **FunnelEffect** and paste the copied text\. 

The following is a sample of a preset contained in the `\dev\Gems\Tornadoes\Assets\libs\MaterialEffects\FXLibs`\\`tornado.xml` file in the Lumberyard root directory \(`lumberyard_version\dev`\)\.

```
 <Particles Name="tornado.leaves">
  <Params Count="35" Continuous="true" ParticleLifeTime="4,Random=0.248" FocusGravityDir="true" EmitAngle="Random=1" OrientToVelocity="true" Texture="textures/sprites/smoke/smoke_b.tif" SoftParticle="true" Alpha="0.267,ParticleAge=(;t=0.055,v=1;t=0.518;t=1)" Color="(x=0.608,y=0.467,z=0.34)" DiffuseLighting="0.554" DiffuseBacklighting="0.494" Size="20,Random=0.812,ParticleAge=(v=1;t=0.51,v=0.25;t=1)" Stretch="0.2" Speed="5" GravityScale="-2" TurbulenceSize="1.699147" TurbulenceSpeed="335.1465" RandomAngles="y=359"/>
  <Childs>
   <Particles Name="base_dirt1">
    <Params Count="44" Continuous="true" ParticleLifeTime="0.35" FocusGravityDir="true" EmitAngle="70" OrientToVelocity="true" Texture="textures/sprites/dirt/dirt_c.tif" SoftParticle="true" Alpha="0.3,ParticleAge=(;t=0.5,v=1;t=1)" Color="(x=0.733,y=0.725,z=0.616)" DiffuseBacklighting="1" Size="120,Random=0.2307692" Speed="180" Turbulence3DSpeed="50" TurbulenceSize="10" TurbulenceSpeed="-35.8" Bounciness="-1" SortOffset="-0.02" VisibleUnderwater="If_False" ConfigMin="Medium"/>
   </Particles>
   <Particles Name="base_smoke1">
    <Params Count="25" Continuous="true" ParticleLifeTime="0.9,Random=0.168" RandomOffset="x=15,y=15" FocusGravityDir="true" EmitAngle="90" OrientToVelocity="true" Texture="textures/sprites/smoke/smoke_tiled_c.tif" TextureTiling="TilesX=2,TilesY=2,VariantCount=4" SoftParticle="true" Alpha="ParticleAge=(;t=0.49,v=1;t=1)" Color="(x=0.73,y=0.62,z=0.52)" DiffuseBacklighting="1" Size="40,Random=0.119,ParticleAge=(v=0.34;t=1,v=1)" Speed="60,Random=0.238" RandomAngles="y=359" RandomRotationRate="y=180" Bounciness="-1" SortOffset="-0.01" ConfigMin="Medium"/>
   </Particles>
   <Particles Name="debris">
    <Params Count="50" Continuous="true" ParticleLifeTime="30,Random=0.3" RandomOffset="x=20,y=20" FocusGravityDir="true" EmitAngle="Random=1" Facing="Free" Texture="textures/sprites/wood/wood_chip_tiled.tif" TextureTiling="TilesX=2,TilesY=2,VariantCount=4" DiffuseBacklighting="1" Size="5,Random=0.317,ParticleAge=(v=0.114;t=1,v=1,flags=4)" Speed="10,Random=0.3,EmitterStrength=(v=0.5;t=1,v=1,flags=4)" GravityScale="ParticleAge=(;t=1,v=1)" TurbulenceSize="60,Random=0.2,ParticleAge=(v=0.09;t=0.663,v=0.23;t=1,v=1,flags=4)" TurbulenceSpeed="-100,Random=0.5" RandomAngles="z=180" RandomRotationRate="x=600,y=600,z=600" FillRateCost="0.2"/>
   </Particles>
   <Particles Name="leaves1">
    <Params Count="50" Continuous="true" ParticleLifeTime="30,Random=0.3" FocusGravityDir="true" EmitAngle="Random=1" Facing="Free" Texture="textures/sprites/leaves/leaf_tiled_a.tif" TextureTiling="TilesX=2,TilesY=2,VariantCount=4" DiffuseBacklighting="1" Size="2,Random=0.317,ParticleAge=(v=0.114;t=1,v=1,flags=4)" Speed="10,Random=0.3,EmitterStrength=(v=0.5;t=1,v=1,flags=4)" GravityScale="ParticleAge=(;t=1,v=1)" TurbulenceSize="60,Random=0.2,ParticleAge=(v=0.09;t=0.663,v=0.23;t=1,v=1,flags=4)" TurbulenceSpeed="-100,Random=0.5" RandomAngles="z=180" RandomRotationRate="x=600,y=600,z=600" FillRateCost="0.2"/>
   </Particles>
   <Particles Name="base_smoke2">
    <Params Count="40" Continuous="true" ParticleLifeTime="6" EmitAngle="3,Random=1" OrientToVelocity="true" Texture="textures/sprites/smoke/smoke_tiled_d.tif" TextureTiling="TilesX=2,TilesY=2,VariantCount=4" SoftParticle="true" Alpha="0.5,Random=0.248,ParticleAge=(;t=0.055,v=1;t=0.996)" Color="(x=0.353,y=0.318,z=0.28),ParticleAge=(v=(x=0.42,y=0.34,z=0.17);t=0.925,v=(x=0.867,y=0.925,z=1))" DiffuseBacklighting="0.3" Size="130,Random=0.188,ParticleAge=(v=0.57,flags=32;t=0.255,v=0.5;t=0.996,v=1,flags=4)" Stretch="0.2,ParticleAge=(t=0.514,v=0.5;t=1,v=1)" Speed="3" GravityScale="-1.6" TurbulenceSize="1.7" TurbulenceSpeed="-120" InitAngles="y=90" RandomAngles="y=180" RotationRate="y=100" RandomRotationRate="y=20" SortOffset="-0.31" FillRateCost="0.7"/>
   </Particles>
  </Childs>
 </Particles>
```