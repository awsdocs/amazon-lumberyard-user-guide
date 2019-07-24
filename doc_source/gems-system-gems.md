# Using Gems to Add Modular Features and Assets<a name="gems-system-gems"></a>

Gems are packages that contain code and assets to augment your game projects\. With the [Programming with Gems](gems-system.md), you can choose the features and assets that you need for your game project without including unnecessary components\. For example, you might add the [Boids Gem](gems-system-gem-boids.md) to create entities for a flock of birds to place in your game\. For a list of all gems included in Lumberyard, see [Gems Available in Lumberyard](gems-system-ref.md)\.

Lumberyard features two types of Gems:
+ **Code & Assets** – Contains assets as well as code that performs certain functions upon the assets\.
+ **Assets Only** – Contains only assets and no code\.

All Lumberyard gems are located in the following directory: 

`lumberyard_version\dev\Gems`

The gems that you enable are automatically detected and built through the integrated [Using the Waf Build System](waf-intro.md)\.

**Note**  
To enable **Code & Assets** Gems, you must select the **Compile the game code** option in Lumberyard Setup Assistant\. This option is not required for **Assets Only** gems\. For more information, see [Running Lumberyard Setup Assistant](lumberyard-launcher-using.md)\.

You can enable gems with the [Project Configurator](configurator-projects.md) or the command line \([`Lmbr.exe`](lmbr-exe.md)\)\.

**Topics**
+ [Enabling Gems](gems-system-using-project-configurator.md)
+ [Creating a Gem](gems-system-gems-creating.md)
+ [Programming with Gems](gems-system.md)
+ [Gems Available in Lumberyard](gems-system-ref.md)
