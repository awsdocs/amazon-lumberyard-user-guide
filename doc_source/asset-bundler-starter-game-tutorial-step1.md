# Step 1: Preparing a Release Build of StarterGame<a name="asset-bundler-starter-game-tutorial-step1"></a>

Set StarterGame as your default project and create a release build for it\.

1. Open the Amazon Lumberyard Project Configurator\.

1. Select **StarterGame** and click **Set as default** in the upper\-right corner of the Project Configurator screen\.  
![\[Setting the StarterGame as the default project from the Project Configurator.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-project-configurator.png)

1. Open a command prompt and navigate to `{Lumberyard Install Root Directory here}\dev`\. Run the following command: lmbr\_waf configure\. 

1. When the WAF configuration for your new project completes, use the **All** build spec to create a profile build\. You configure this by providing the value `all` to the `-p` parameter of lmbr\_waf\. Open a command prompt and run the following command: lmbr\_waf build\_win\_x64\_vs2017\_profile \-p all\.

   This step ensures that your editor, asset processor, asset builders, and other edit\-time content is up to date\. It is also necessary for shader generation\.

1. Make a release build of the game\_and\_engine build spec\. Open a command prompt and run the following command: lmbr\_waf build\_win\_x64\_vs2017\_release \-p game\_and\_engine\.

1. Open Lumberyard Editor and select **Game** > ** Play Game** \(or press Ctrl\+G\) to enter Game mode\. Roam the player around the level to pick up the shader references\. Then export it by selecting **Game** > **Export to Engine** from the main menu, or pressing Ctrl\+E\.  
![\[Opening the StarterGame level in the editor for export.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-level-in-editor.png)

You now have a release build for StarterGame located in your `{Lumberyard Install Root Directory Here}\dev\Bin64vc141.Release\` folder\. 

![\[An example initial release build directory.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-release-build.png)

## Next Step<a name="asset-bundler-starter-game-tutorial-step1.2"></a>

 [Step 2: Define the basic directory structure for your release](asset-bundler-starter-game-tutorial-step2.md) 