# Testing Your Gem<a name="gems-system-gems-testing"></a>

After you move your assets into the gem's directory structure, you can enable your new Gem in your game project and then test it in Lumberyard\.

**To enable and test your new Gem**

1. Open the Project Configurator by doing one of the following:
   + Open Lumberyard Setup Assistant\. On the **Summary** page, click **Configure project**\.
   + Navigate to the `lumberyard_version\dev\Bin64vc140\` directory (if using Visual Studio 2015), or the `lumberyard_version\dev\Bin64vc141\` directory (if using Visual Studio 2017) and then start `ProjectConfigurator`\.

1. [Enable](gems-system-using-project-configurator.md) your new Gem\.

1. Close the **Project Configurator**\.

1. Launch Lumberyard and open a level\.

1. Use the **Asset Browser** to place the gem's assets into your scene\. Verify that your assets look as intended\. If they do not, verify that you have set up the directories correctly\.
