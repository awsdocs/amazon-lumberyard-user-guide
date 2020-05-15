# **NVIDIA Cloth Gem**<a name="gems-system-gem-nv-physx-cloth"></a>


****  

|  | 
| --- |
| This feature is an [experimental](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#experimental) release and is subject to change\.  | 

![\[NVIDIA Cloth Gem in Amazon Lumberyard.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/nvidiacloth/anim-nvidia-cloth-lyflag-1.23.gif)

Physical cloth simulations can create more immersive environments and characters\. The **NVIDIA Cloth Gem** uses the **NVIDIA Cloth** library to provide fast, robust cloth simulation in Amazon Lumberyard\.

**Note**  
The **NVIDIA Cloth Gem** is currently available only for Windows\. 

## Enable the **NVIDIA Cloth Gem**<a name="enable-gem-cloth"></a>

Cloth simulations are created through a familiar, intuitive component that you can add to entities that contain **Mesh** or **Actor** components\. To make the **Cloth** component available in Lumberyard, you must build and configure your project with the **NVIDIA Cloth Gem** enabled\. 

1. Use Project Configurator to add the **NVIDIA Cloth Gem** to your project\. 
**Note**  
The **NVIDIA Cloth Gem** also requires the **LmbrCentral** and **EmotionFX** gems\. 

1. Configure your project\. 

   **lmbr\_waf configure** 

1. Build your project\. 

   **lmbr\_waf build\_*win\_x64\_vs2017*\_profile \-p all** 

For more information, see the [Gems documentation](gems-system-gems.md)\. 

**Topics**
+ [Enable the **NVIDIA Cloth Gem**](#enable-gem-cloth)
+ [Cloth Component](component-cloth.md)
+ [Cloth Simulation](tutorial-cloth-simulation.md)
+ [Create Cloth for Environments](tutorial-cloth-environment.md)
+ [Create Cloth for Characters](tutorial-cloth-characters.md)