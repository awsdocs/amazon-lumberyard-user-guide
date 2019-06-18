# Starter Game Sample<a name="sample-level-starter-game"></a>

You can use the Starter Game sample to see how Lumberyard systems work together to make a game\. Starter Game is a small, third\-person game that is built with the Lumberyard component entity system\. In addition to component entities, Starter Game demonstrates bipedal locomotion, voxel\-based global illumination, the time of day system, and more\. In this sample, you play as Jack, a robot that has crashed on a distant planet\. Jack can explore the world and must defend himself against enemy robots that occupy the planet\. You can use Jack or any other assets in the Starter Game sample to prototype your own projects\.

You can get the Starter Game sample from the following sources:
+ Lumberyard package \(Lumberyard 1\.11 and newer\)

  The Starter Game sample is included in the engine package\.
+ [Lumberyard Downloads](https://aws.amazon.com/lumberyard/downloads/) page

  The Starter Game sample download includes the latest features and improvements that aren't yet integrated into the sample in the engine package\. An example is the Starter Game Action Update\.
+ [Legacy Downloads](https://aws.amazon.com/lumberyard/downloads/previous-versions/) page

  The download includes the Starter Game sample that is supported in the previous version of Lumberyard\. For example, if the newest version is Lumberyard 1\.11, this download is supported in Lumberyard 1\.10\.

**Note**  
The Starter Game sample now supports the following platforms:  
Windows
macOS
iOS
Android \(for good performance, use devices no older than 2 years with ARMv8 and Adreno GPU\)

If you have been making your own changes to Starter Game and don't want to lose your work when upgrading to a newer release of Lumberyard, see [Upgrading Your Starter Game Project](lumberyard-migrating-1-10.md#lumberyard-migrating-1-10-starter-game)\.

![\[Starter Game sample for Lumberyard.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/starter-game-1.jpg)

**To install the Starter Game sample \(if not yet installed\)**

1. From the [Downloads](https://aws.amazon.com/lumberyard/downloads/) page, download the `StarterGame.zip` package\.

1.  Extract the package to your Lumberyard directory: for example, `\Lumberyard\1.x.0.0`\.

1. Double\-click the Project Configurator desktop icon\.

1. In the Project Configurator, select **Starter Game**\.

1. Click **Set as default** and close the Project Configurator\.

1. Double\-click the Lumberyard Editor desktop icon\.

1. In the **Welcome to Lumberyard Editor** dialog box, click **Open level**\.

1. In the **Open a Level** dialog box, select **StarterGame** and click **Open**\.

1. To start the game, press **Ctrl\+G**\. 

1. Use the following keyboard keys and mouse controls:
   + To move forward, strafe left, move backward, and strafe right, press the **W**, **A**, **S**, and **D** keys, respectively\.
   + To look around, move the mouse\.
   + To shoot, click the primary mouse button\.
   + To toggle weapon selection, click the secondary mouse button\.
   + To toggle time of day, press the **<** key\.

     For more information about the time of day settings, see [Creating Time of Day Sky Effects](sky-tod-intro.md)\.
   + To change the antialiasing mode, press the **>** key\.

     For more information about antialiasing, see [Controlling Antialiasing](graphics-rendering-anti-aliasing.md#graphics-rendering-anti-aliasing-antialias)\.
   + To exit the game, press **Esc**\.

   If you're running Starter Game in the editor and Jack the robot dies, press **Esc** to exit the game\.
**Note**  
By default, the viewport window displays debugging information when you're in gameplay mode \(**Ctrl\+G**\)\. To toggle this information on or off, press the tilde \(**\~**\) key\. For more information, see [Using Console Debug Views](debugging-intro.md#debugging-debug-views)\.