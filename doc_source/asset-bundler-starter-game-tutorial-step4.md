# Step 4: Generate auxiliary data<a name="asset-bundler-starter-game-tutorial-step4"></a>

Generate the auxiliary data, and move that data into your release build bundle directory\. This includes Gem data, configuration info, and level data and packages\. 

1. Open a command prompt\. Run the following batch file to generate the auxiliary data that you need to finish preparing your bundle: `Build_AssetBundler_AuxiliaryContent_PC.bat --game StarterGame`

   [Download](https://d1a5h15s88ekwk.cloudfront.net/1.22.0.0/scripts/Build_AssetBundler_AuxiliaryContent_PC.bat) the `Build_AssetBundler_AuxiliaryContent_PC.bat` if it is not available\.

   Running this file places the auxiliary data into a directory called `startergame_pc_paks` under `{Lumberyard Install Root Directory here}\dev`\.

1. Copy the contents of `startergame_pc_paks` into your `startergame` release build subdirectory\.   
![\[The release build directory structure for StarterGame with the auxiliary data included.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-full-structure.png)

   Shut down the shader compile server in the command line window you opened at the beginning of this step\.

## Next Step<a name="asset-bundler-starter-game-tutorial-step4.1"></a>

 [Step 5: Generate the asset bundle](asset-bundler-starter-game-tutorial-step5.md) 