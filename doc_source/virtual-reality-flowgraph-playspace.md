# Setting Up a Custom Playspace with Flow Graph<a name="virtual-reality-flowgraph-playspace"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can use flow graph to set up a custom playspace for OpenVR \(Vive HTC head\-mounted display \[HMD\]\)\.

When a user first sets up their Vive HTC HMD, they must configure their playspace, or play area, according to their available space and room configuration\. You can set up a flow graph to enable your game to access this information in order to spawn game objects within the user's reach and to create a visual area for the user to move within\.

Lumberyard has included a sample virtual reality level\. Open **VR\_BoxGarden\_Sample** in the [Samples Project](sample-project-samples.md)\. You may copy or modify this sample level for your own uses\.

The following pictures show examples of:
+ **A** – 2m x 2m playspace
+ **B** – 4m x 3m playspace

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-playspace-area.png)

The following pictures show examples of spawning posts around the perimeter of a playspace with an area of:
+ **C** – 2m x 2m
+ **D** – 4m x 3m

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-playspace-area-spawn.png)

The following flow graph from **VR\_BoxGarden\_Sample** in the [Samples Project](sample-project-samples.md) shows an example of how to scale the user playspace to create the box shown in the above pictures\. This flow graph uses the user playspace width \(x\) and length \(y\), and scales the height \(z=0\.1\) to create an area equivalent to the user playspace, but at the height of a floorboard\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/virtual-reality-flowgraph-playspace-graph.png)