# Simple Asset Bundling and Release Tutorial<a name="asset-bundler-tutorial-simple"></a>

This tutorial shows you how to create a simple Lumberyard game project and release build that uses asset bundling for game and engine content\. In this tutorial, you complete the following steps: 
+ Create a new game project in Lumberyard\.
+ Create a release build of your new game's executable\.
+ Set up a directory structure for your release build\.
+ Generate shader and auxiliary data for your release build\.
+ Create bundled content using the new asset bundling system\.
+ Update and run your release build and verify that it works\.

## Prerequisites<a name="asset-bundler-tutorial-simple-prerequisites"></a>

To complete the procedures in this tutorial, make sure that you have the following set up: 
+ Amazon Lumberyard v1\.22 or later installed\. [Download the latest version of Amazon Lumberyard](https://aws.amazon.com/lumberyard/downloads/)\.
+ Lumberyard v1\.22 or later configured so that it can compile your game, and also Lumberyard Editor and the Lumberyard engine\. [Learn more about setting up Lumberyard](setting-up-intro.md)\.
+ Optionally, familiarity with some of the concepts and terminology presented in this tutorial\. [Learn more about Asset Bundler Concepts](asset-bundler-concepts.md)\.

## Create a Game Project<a name="asset-bundler-tutorial-simple-create-project"></a>

In this step, create a new Simple game project\.

1. Open Lumberyard and launch the Project Configuration\.

1. Select **Create a new project** and choose the **Default** template\.

1. After your project is created, make sure the project is selected, and click **Set as default**\.

1. Click **Enable Gems** to open **Gem management**\.

1. Search for the **Asset Validation** gem and click the check box to enable it for your game\. This gem is used to verify that your builds include all of the assets that you need\. 

1. Click **Save**\.

## Create a Release Build<a name="asset-bundler-tutorial-simple-create-release"></a>

1. Open a command prompt and navigate to the Lumberyard install root directory\. 

1. Configure the Waf build system using the following command\. For more information about Waf configuration options, see [Waf Configuration](waf-commands.md#waf-configuration)\. 

   ```
   lmbr_waf configure
   ```

1. Create a profile build using the **All** build spec by running the following command\. This step ensures that your editor, asset processor, asset builders, and other edit\-time content is up to date\. It is also necessary for shader generation\.

   ```
   lmbr_waf build_win_x64_vs2017_profile -p all
   ```

1. Make a release build of the game\_and\_engine build spec with the following command\.

   ```
   lmbr_waf build_win_x64_vs2017_release -p game_and_engine
   ```

1. Open Lumberyard Editor, load the **Simple** level in the editor, and then export it\. You can export the level using the keyboard shortcut **Ctrl\+E**, or the menu option **Game:Export to Engine**\. This step ensures that the level is up to date in the release build after you perform asset bundling\.

You now have created a release build from your Simple game project and exported a level\.

## Define a Release Bundle Directory Structure<a name="asset-bundler-tutorial-simple-build-directory"></a>

After you create a sample game project, define the basic directory structure for your release setup and copy the release build into it\.

1. Create a folder for your release build\. We recommend that you do not make this a subdirectory under your engine root\. By creating this release directory outside of your development folder, it helps verify that your release build contains release content only, and not development content\.

1. Create a subfolder for your release build, including release binaries and executables\. For example, you might name this subfolder "Release\." 

1. Create a peer subfolder for your game's content\. Name this folder using the name of the game folder in the engine root directory\. For example, you might name this subfolder "assetbundlingdemo"\. 

1. Locate the release build that you generated in the previous section and copy it into the new release build subfolder\.

## Generate Shaders and Auxiliary Data<a name="asset-bundler-tutorial-simple-build-shaders"></a>

Build the shader assets and auxiliary data for your game and add them to your release build bundle directory that you created in the previous section\.

1. If your remote shader compile server is running, obtain the shader list \(called `shaderlist.txt`\) from it\. Otherwise, you must generate one by opening Lumberyard Editor, moving the camera around the initial Simple level until you've generated all the shaders locally\. When you're finished, close the editor\.

1. Open a command prompt and navigate to `{Lumberyard Install Root Directory here}\dev\Tools\CrySCompileServer\profile\`\.

1. Start the local shader server process using the following command\. **Do not close the command prompt\.**

   ```
   CrySCompileServer.exe
   ```

1. Open a second command prompt window and launch your Simple game using the following command\. Replace `<AssetBundlingDemo>` with the name of your game project\. As this process progresses, the shader server that your started in Step 3 generates `.pak` files for your shaders\. The path is provided in the command output\. 

   ```
   lmbr_pak_shaders.bat <AssetBundlingDemo> D3D11 pc
   ```

1. Once the process in Step 4 is completed, you can stop the local shader server that was started in Step 3\.

1. Go to the path where the shader `.pak` files were generated in the previous step\. Select these files and copy them into the root of the game content subfolder of the release bundle that you created in the previous section\.

1. Open a new command prompt and run the following command\. This batch file generates the auxiliary data, including Gem data, configuration information, and level data and packages that your need to finish prepping your bundle\.

   ```
   Build_AssetBundler_AuxiliaryContent_PC.bat --game <AssetBundlingDemo>
   ```

   [Download](https://d1a5h15s88ekwk.cloudfront.net/1.22.0.0/scripts/Build_AssetBundler_AuxiliaryContent_PC.bat) the `Build_AssetBundler_AuxiliaryContent_PC.bat` if it is not available\.
   
   Auxiliary data is generated in the directory `{Lumberyard Install Root Directory here}\dev\<AssetBundlingDemo>_pc_paks`\.

1. Copy the contents of `<AssetBundlingDemo>_pc_paks` into the root of the game content subfolder of the release bundle that you created in the previous section\.

## Generate Asset Bundles<a name="asset-bundler-tutorial-simple-generate-bundles"></a>

Generate the final bundle for deployment using the `AssetBundlerBatch.exe` command line tool\. 

This sections describes how to generate two sets of content, one for your engine content and one for your game content\. This approach works well for games where game content changes frequently while engine content changes rarely\. For your game, you might choose to combine content into a single bundle or generate multiple bundles\.

1. Open a command prompt and navigate to the game content subfolder in your release build bundle directory\.

1. To create your engine content files, run the following commands: 

   ```
   Bin64vc141\AssetBundlerBatch.exe assetLists --addDefaultSeedListFiles --assetListFile engine.assetlist
   Bin64vc141\AssetBundlerBatch.exe bundles --assetListFile engine_pc.assetlist --outputBundlePath engine.pak
   ```

   Content is generated as `Engine_pc.pak` file\.

1. To create your engine content files, run the following commands: 

   ```
   Bin64vc141\AssetBundlerBatch.exe seeds --addSeed levels\simple\level.pak --addSeed project.json --addSeed gems.json --seedListFile mygameseeds.seed
   Bin64vc141\AssetBundlerBatch.exe assetLists --seedListFile mygameseeds.seed --assetListFile mygameassets.assetlist
   Bin64vc141\AssetBundlerBatch.exe bundles --assetListFile mygameassets_pc.assetlist --outputBundlePath mygame.pak
   ```

   Content is generated as `MyGame_pc.pak` file\. 

1. Copy the content `.pak` files into the root of the game content subfolder of the release bundle that you created in a previous section\.

## Run Your Release Build With Asset Bundles<a name="asset-bundler-tutorial-simple-update-release"></a>

Now that you've generated your release build files and content files, test your work by running your project build\. 

1. Open a command prompt and navigate to your release build directory\.

1. Run the launcher executable for your games\. This build won't load a map by default, so make sure to specify a map as illustrated in the following command\.

   ```
   <AssetBundlingDemo>Launcher.exe +map simple
   ```

If your content bundles are correct, you'll see a scene showing a set of 3D shapes with a checkerboard texture\. If the shapes are displayed but the texture is missing, it probably means you did not export the level before creating the release build\.

If the test isn't successful, common issues may occur\. For example, error messages may display, the launcher may shut down, or a black screen displays\. For more information about troubleshooting common issues, see [Resolving Missing Assets](asset-bundler-assets-resolving.md) and [Compiling Shaders for Release Builds](asset-pipeline-shader-compilation.md)\.

**Note** 

When you run the release build, it creates a `User` subdirectory under your release build directory\. Be sure to delete this directory before shipping the release build\.

## Next Steps<a name="asset-bundler-tutorial-simple-next-steps"></a>

Now that you've walked through the basics of creating release builds with asset bundles, you may want to explore the following topics:
+ Learn about how bundles are mounted, so that you can load content dynamically\. See [Creating Multiple Asset Bundles](asset-bundler-tutorial-multiple-bundles.md)
+ Explore the asset bundler functionality\. See [Lumberyard Asset Bundler Command\-Line Tool Reference](asset-bundler-command-line-reference.md)\.
+ Learn how to scan for missing dependencies in your bundles\. See [Using the Missing Dependency Scanner](asset-bundler-missing-dependency-scanner.md)
+ To ask questions about the Asset Bundler and get support, see [the Amazon Lumberyard forums](https://forums.awsgametech.com/)\. 