# Creating Content Patch Bundles with Lumberyard<a name="asset-bundler-tutorial-content-patches"></a>

This tutorial demonstrates a bundling process designed to simulate the common use case of games that experience frequent content updates\. In this tutorial, you create a set of bundles that simulates a content patch update\. The update contains only content that changed since the first set of bundles was created\. This topic covers:
+ Modifying an asset reference to reference a new asset that was not bundled previously\.
+ Creating an updated asset bundle that contains only updated or new assets\.
+ Running the new release build with new bundles\.

## Prerequisites<a name="asset-bundler-tutorial-content-patches-prerequisites"></a>

To complete this tutorial, you should have completed [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md), the [Creating Multiple Asset Bundles](asset-bundler-tutorial-multiple-bundles.md) tutorial, and the prerequisites in both\.

## Tutorial<a name="asset-bundler-tutorial-content-patches-tutorial"></a>

In this tutorial, modify the second level from the [multiple bundles tutorial](asset-bundler-tutorial-multiple-bundles.md) to simulate a content update, refresh the bundles, and simulate the user experience after the update\.

### 1\. Modify level2 from the Previous Level<a name="asset-bundler-tutorial-content-patches-modify-level2-from-the-previous-level"></a>

**To modify the second level**

1. Launch Lumberyard Editor, and then close the welcome screen\. Do not load a level\.

1. Choose **Tools**, **Material Editor**\.

1. Select the `level2material.mtl` file\.

1. Change the diffuse texture to `materials\pbs_reference\coal_diff.dds`\.

1. Choose **Save** to save the material\.

### 2\. Refresh the Unchanged Bundles<a name="asset-bundler-tutorial-content-patches-refresh-the-unchanged-bundles"></a>

While refreshing unchanged bundles might be unnecessary, doing so can be faster than trying to determine which specific bundles need to be refreshed\.

The following procedure shows how to refresh the engine bundle\. The steps for refreshing the *mygame* bundle are similar\.

**To refresh the engine bundle**

1. Run the following commands, which have been formatted for readability\.

   ```
   Bin64vc141\AssetBundlerBatch.exe assetLists ^
       --addDefaultSeedListFiles ^
       --assetListFile engine_all_v2.assetlist
   ```

   ```
   Bin64vc141\AssetBundlerBatch.exe compare ^
       --comparisonType delta ^
       --firstAssetFile engine_v1_pc.assetlist ^
       --secondAssetFile engine_all_v2_pc.assetlist ^
       --output engine_pruned_v2.assetlist
   ```

   Because you want to include modified assets in the bundle, the previous command uses the *delta* comparison type, not the *complement* type used in the [Creating Multiple Asset Bundles](asset-bundler-tutorial-multiple-bundles.md) tutorial\. For more information, see [Amazon Lumberyard Asset List Comparison Operations](asset-bundler-list-operations.md)\.

1. Open the `engine_pruned_v2.assetlist` file in a text editor\. If you haven't changed any engine or gem content since you completed the last tutorial, the asset list will have no files\. If so, you do not need to generate an updated `.pak` file\. The following example shows an empty asset list\.

   ```
   <ObjectStream version="3">
       <Class name="AssetFileInfoList" version="1" type="{61F16042-E381-47E4-8AAA-91BC532F4101}">
           <Class name="AZStd::vector" field="fileInfoList" type="{4F6B07E0-7EB7-5CE4-AABE-8717224FC1DB}"/>
       </Class>
   </ObjectStream>
   ```

### 3\. Refresh the Changed Bundle<a name="asset-bundler-tutorial-content-patches-refresh-the-changed-bundle"></a>

Now you are ready to refresh the changed bundle\.

**To refresh the changed bundle**

1. Run the following commands, which have been formatted for readability\.

   ```
   Bin64vc141\AssetBundlerBatch.exe assetLists ^
       --seedListFile dlc_level2.seed ^
       --assetListFile dlc_level2_all_v2.assetlist
   ```

   ```
   Bin64vc141\AssetBundlerBatch.exe compare ^
       --comparisonType complement ^
       --firstAssetFile engine_v1_pc.assetlist ^
       --secondAssetFile dlc_level2_all_v2_pc.assetlist ^
       --output dlc_level2_pruned_v2.assetlist
   ```

   ```
   Bin64vc141\AssetBundlerBatch.exe compare ^
       --comparisonType complement ^ 
       --firstAssetFile mygameassets_pruned_v1_pc.assetlist ^
       --secondAssetFile dlc_level2_pruned_v2_pc.assetlist ^
       --output dlc_level2_pruned_v2.assetlist ^
       --allowOverwrites
   ```

1. Run the following command, which differs from the previous tutorial\. The command has been formatted for readability\.

   ```
   Bin64vc141\AssetBundlerBatch.exe compare ^
       --comparisonType delta ^
       --firstAssetFile dlc_level2_pruned_v1_pc.assetlist ^
       --secondAssetFile dlc_level2_pruned_v2_pc.assetlist ^
       --output dlc_level2_delta_v1_to_v2.assetlist
   ```

1. Run the following command, which has been formatted for readability\.

   ```
   Bin64vc141\AssetBundlerBatch.exe bundles ^
       --assetListFile dlc_level2_pruned_v2_pc.assetlist ^
       --outputBundlePath dlc_level2_v2.pak
   ```

1. Run the following command, which differs from the previous tutorial\. The command has been formatted for readability\.

   ```
   Bin64vc141\AssetBundlerBatch.exe bundles ^
       --assetListFile dlc_level2_delta_v1_to_v2_pc.assetlist ^
       --outputBundlePath z_dlc_level2_delta_v1_to_v2.pak
   ```

   Because the default `.pak` file mounting order mounts bundles in alphabetical order, the file name in the previous command is purposely named to appear after the other `.pak` files\. By default, when multiple assets with the same asset ID exist in multiple packages, the asset is loaded from the most recently mounted `.pak` file\. You can modify this behavior in the Lumberyard engine source code or use an asset bundle naming scheme that uses alphabetical order\.

#### Two Unique Bundles<a name="asset-bundler-tutorial-content-patches-two-unique-bundles"></a>

The last two commands of the procedure created two unique asset bundles for the downloadable level: `dlc_level2_v2.pak` and `z_dlc_level2_delta_v1_to_v2.pak`\.

The first asset bundle, `dlc_level2_v2.pak`, contains all content that level2 has in the v2 revision of the game\. You can build your content download system to distribute this to players who load this level for the first time\.

The second asset bundle, `z_dlc_level2_delta_v1_to_v2.pak`, contains only the content that changed in level2 between v1 and v2 of your game\. Players who already have the v1 asset bundle for this level require only this delta package to have all the content required for v2 of your game\.

### 4\. Simulate the User Scenarios<a name="asset-bundler-tutorial-content-patches-simulate-the-user-scenarios"></a>

Now you are ready to simulate two scenarios: users who have v1 of your game but upgrade to v2, and users who download v2 for the first time\.

#### Simulating the v1 to v2 patch experience<a name="asset-bundler-tutorial-content-patches-simulating-the-v1-to-v2-patch-experience"></a>

For this part of the tutorial, you're going to simulate the user experience of downloading the delta patch\.

At this point, your release build directory should be identical to how it was at the end of the previous tutorial\. If not, restore it to its previous state\. As a reminder, the release build directory should appear similar to the following image\.

![\[Release build directory original state.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-1.png)

**To simulate the v1 to v2 delta patch experience**

1. To confirm the previous behavior, run your game without the updated asset bundle file\.  
![\[Running the game to show previous content.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-2.png)

1. Place the `z_dlc_level2_delta_v1_to_v2.pak` file in your release build, as shown in the following image\.  
![\[Placing the v2 .pak file in the release build directory.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-3.png)

1. To view the updated v2 content, run the game\.  
![\[The game launched with updated v2 content.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-4.png)

#### Simulating the v2 download experience<a name="asset-bundler-tutorial-content-patches-simulating-the-v2-download-experience"></a>

The following procedure simulates the experience for a user who downloads v2 of your game content for the first time\.

**To simulate the v2 download experience**

1. To return to the base v1 package, delete the patch asset bundle from your release build\.

1. Delete the v1 package for your level 2\.

   The following image shows the files to delete\.  
![\[Files to delete before simulating the v2 download experience.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-5.png)

1. Place the v2 level asset bundle into the release package where the previous v1 bundle was\.

   The following image shows where the file should be added\.  
![\[Placing the v2 asset bundle into the release.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-6.png)

1. Use the launcher to run the level for your game, as shown in the following command\.

   ```
   AssetBundlingDemoLauncher.exe +map level2
   ```

   The v2 version of your game content is displayed, as shown in the following image\.  
![\[The game launched for the first time with v2 content.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-content-patches-7.png)

## Conclusion<a name="asset-bundler-tutorial-content-patches-conclusion"></a>

You have now tried two different methods of patching content for a Lumberyard game\. The steps in these workflows are flexible\. You can change them to meet your needs\.