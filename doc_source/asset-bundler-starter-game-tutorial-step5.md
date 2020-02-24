# Step 5: Generate the asset bundle<a name="asset-bundler-starter-game-tutorial-step5"></a>

Generate the final bundle for deployment using the `AssetBundlerBatch.exe` command line tool\. 

1. Open a command prompt and navigate to the `startergame` directory in your release build directory\.

1. Run AssetBundlerBatch\.exe assetLists \-\-addSeed=levels\\startergame\\level\.pak \-\-seedListFile=StarterGame\\Levels\\StarterGame\\SeedAssetList\.seed \-\-assetListFile=StarterGame\\AssetListFiles\\startergame\.assetlist \-\-addDefaultSeedListFiles at the prompt\. This command builds the `.assetlist` files that contain the set of dependent product assets\.

1. Run AssetBundlerBatch\.exe bundles \-\-assetListFile=StarterGame\\AssetListFiles\\startergame\_pc\.assetlist \-\-outputBundlePath=StarterGame\\Bundles\\startergame\.pak at the prompt\. This command builds the `.pak` file for deployment using the asset list files generated from the previous step\. If this command builds successfully, the StarterGame is ready for deployment\!

**Step 4\.**

Go ahead and start your build and test it\. 

Open a command prompt, navigate to your release build directory, and run StarterGameRelease\\Release\\StarterGameLauncher\.exe \+map startergame\. 

**Note** 

When you run the release build to test it, it creates a `User` subdirectory under your release build directory\. You don't want to include this in your package that you ship to customers, so delete it after testing\.

If your release build test is successful, you'll see this scene:

![\[The screen shown if your package was bundled correctly for deployment.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-starter-game-release.png)

If the test isn't successful, common issues may occur\. For example, error messages may display, the launcher may shut down, or a black screen displays\. For more information about troubleshooting common issues, see [Resolving Missing Assets](asset-bundler-assets-resolving.md) and [Compiling Shaders for Release Builds](asset-pipeline-shader-compilation.md)\.