# Creating Multiple Asset Bundles<a name="asset-bundler-tutorial-multiple-bundles"></a>

The [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md) provided a quick start on using the asset bundling system\. However, it doesn't represent what most games require\. In this tutorial, you learn the bundling process for a common use case: games that download additional content after the player launches the game\. The tutorial shows you how to create a release build with multiple game levels in separate asset bundles that have the contents of the base game removed\.

This topic covers the following points:
+ Adding additional content to the project from the [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md)\.
+ Creating multiple asset bundles separated by game level\.
+ Running the new build with and without the additional bundles\.

## Prerequisites<a name="asset-bundler-tutorial-multiple-bundles-prerequisites"></a>

To complete this tutorial, you should have completed [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md) and its prerequisites\.

## Tutorial<a name="asset-bundler-tutorial-multiple-bundles-tutorial"></a>

In this tutorial, you create a second level, create bundles, and simulate downloading additional content\.

### 1\. Create a Second Level<a name="asset-bundler-tutorial-multiple-bundles-create-a-second-level"></a>

For this phase of the tutorial, create a level that contains an object that references a visible asset\. Using a visible asset lets you compare asset bundles that were created for different levels and have different asset references\.

To accomplish this, place an entity with a mesh component in front of a camera, create a new material, and assign a material override to the mesh\. If you're using your own project, feel free to use names or assets that are different from those used here\.

**To create a second level**

1. Launch the editor, and create a second level\. Name it **level2**\.  
![\[Creating a new level in Lumberyard Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-1.png)

1. Create a camera\. Right\-click the **Perspective** button, and choose **Create camera entity from current view**\.  
![\[Choose Create camera entity from current view.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-2.png)

1. In view of the camera, create an entity with a mesh component\.

1. In the Asset Browser, search for the **\_Box\_1x1\.cgf** mesh\. Drag the box mesh into the viewport, assigning it to the entity with the mesh component\.  
![\[Assigning a box mesh to an entity in the viewport.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-3.png)

1. Choose **Tools**, **Material Editor**\.  
![\[Choose Tools, Material Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-4.png)

1. From the **Material Editor** toolbar, choose **Add new item** to create a new material\.  
![\[Creating a new material in the Material Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-5.png)

1. Save the material in your project's root directory as `level2material.mtl`\.  
![\[Saving the material as level2material.mtl.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-6.png)

1. From the **PBSReferenceMaterials** gem, assign the **concrete\_stucco\_diff\.dds** texture to the material\.

   1. Next to the **Diffuse** texture input box, choose the \[**\.\.\.**\] icon\.

   1. In the **Pick Texture** search box, search for **concrete**\.

   1. Choose the **concrete\_stucco\_diff\.tif** file\.

   1. Choose **OK**\.  
![\[Assigning a concrete texture to the material.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-7.png)

   1. Choose **Save**\.  
![\[Choose the Save icon in the Material Editor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-8.png)

1. Assign the **level2material** to the material override on the entity with the mesh component\.

   1. Select the entity with the mesh component\.

   1. For **Material override**, choose the \[**\.\.\.**\] icon\.

   1. In the **Pick Material** dialog box, choose the **level2material**\.

   1. Choose **OK**\.  
![\[Assigning the level2material to the entity with the mesh component.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-9.png)

1. Choose **File**, **Save**, or press **Ctrl\+S** to save your level\.

1. Choose **Game**, **Export to Engine**, or press **Ctrl\+E** to export the game\.
**Note**  
Game launchers and the release build use the level that is generated when you export to engine\. This step is possible to miss in some workflows\. If content creators frequently forget this step, it can be automated using Lumberyard Editor's batch mode and Python binding interface\.

1. Verify that your level has been correctly exported and looks as expected\. Run the launcher command, as shown in the following example, for a profile or debug build of your game\.

   ```
   Bin64vc141\assetBundlingDemoLauncher.exe +map level2 
   ```  
![\[Running the launcher for the exported level.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-10.png)

1. Exit the editor\.

### 2\. Create Bundles<a name="asset-bundler-tutorial-multiple-bundles-create-bundles"></a>

In this section, make the following changes in bundle creation from the previous [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md):
+ Remove duplicated content from bundles\.
+ Generate a separate bundle for this new level to simulate downloading content into a released game\.
+ Add versioning information to file names for use in the next tutorial\.

#### Removing Duplicate Content<a name="asset-bundler-tutorial-multiple-bundles-removing-duplicate-content"></a>

In the previous tutorial, you created two `.pak` files: `Engine_pc.pak` and `MyGame_pc.pak`\.

If you unpack these files, or compare the asset lists, you might notice that some files are duplicated in both bundles\. The following image shows the unpacked archives viewed in a comparison tool\. The tool shows files that are identical in both directories\.

![\[Duplicate files in the engine and game bundles.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-11.png)

Lumberyard handles this duplication without issue by prioritizing the loading of `.pak` files based on how they are mounted\. For more information, see [CryPak Details](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/file-access-crypak-accessing-details.html)\. However, because bandwidth and storage space can be at a premium for players, you should minimize duplicated content\.

**To delete the previous `.pak` files**
+ Delete the `engine_pc.pak` and `mygame_pc.pak` asset bundles that you generated in the previous tutorial\.  
![\[Delete the .pak file bundles from the previous tutorial.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-12.png)

#### Generating New Bundles<a name="asset-bundler-tutorial-multiple-bundles-generating-new-bundles"></a>

Now you're ready to generate the following new bundles:
+ A versioned engine asset bundle
+ A versioned game asset bundle file with the contents of the engine asset bundle removed
+ An asset bundle for the new level

**To create a versioned engine asset bundle file**

1. Run the following commands\.

   ```
   Bin64vc141\AssetBundlerBatch.exe assetLists --addDefaultSeedListFiles --assetListFile engine_v1.assetlist 
   ```

   ```
   Bin64vc141\AssetBundlerBatch.exe bundles --assetListFile engine_v1_pc.assetlist --outputBundlePath
               engine_v1.pak
   ```

1. Place the generated bundle in your release build directory `\assetBundlingDemo`, where `assetBundlingDemo` is your game's name\.

Next, you'll create a versioned game asset bundle file with the contents of the engine asset bundle removed\. You're going to use the seed list created in the previous tutorial to create an asset list, so you don't need to generate a new seed list for your game's base package\.

**Note**  
Storing versioned asset list files on disk makes it easier to compare asset lists for different releases, while seed lists are better managed by project version control\.

**To create a versioned MyGame asset bundle file with the contents of the engine asset bundle removed**

1. Run the `assetLists` command to add the assets specified by the `mygameseeds.seed` file to the `mygameassets_all_v1` asset list\.

   ```
   Bin64vc141\AssetBundlerBatch.exe assetLists --seedListFile mygameseeds.seed --assetListFile mygameassets_all_v1.assetlist 
   ```

1. Run the `compare` command to compare the first asset list to the second asset list\. The command creates a third asset list that contains only the files from the second list that are unique\. This step uses the asset list comparison feature of the asset bundler\. For more information, see [Amazon Lumberyard Asset List Comparison Operations](asset-bundler-list-operations.md)\.

   ```
   Bin64vc141\AssetBundlerBatch.exe compare --comparisonType complement --firstAssetFile engine_v1_pc.assetlist --secondAssetFile mygameassets_all_v1_pc.assetlist --output mygameassets_pruned_v1.assetlist
   ```

1. Run the following command to generate a versioned game asset bundle that does not have the contents of the engine asset bundle\.

   ```
   Bin64vc141\AssetBundlerBatch.exe bundles --assetListFile mygameassets_pruned_v1_pc.assetlist --outputBundlePath
               mygame_v1.pak
   ```

1. Place the generated bundle in your release build directory `\assetBundlingDemo`, where `assetBundlingDemo` is your game's name\.

1. Compare the contents of the two updated `.pak` files\. Note how none of the files in `mygame_v1_pc.pak` and `engine_v1_pc.pak` are the same\.

Regenerating auxiliary data is necessary because some level data exists in the auxiliary data\. While you could perform the same auxiliary generation steps as the previous tutorial, in this case you have a single level that you know has been added\.

**To regenerate auxiliary data**

1. In your release build's content directory, under the `levels` directory, create a new directory named `level2`\.

1. Copy the `level.pak` and the `terraintexture.pak` files into this directory\.  
![\[Copying bundles into the level2 directory.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-13.png)

If you want to add new levels to a game using downloadable content, follow this pattern in your content downloading logic\. If you want to refresh other files that might require updating, you can use the technique in the first tutorial to regenerate auxiliary data\.

Now you are ready to create an asset bundle for the new level\.

**To create an asset bundle for the new level**
+ Run the following commands:

  ```
  Bin64vc141\AssetBundlerBatch.exe seeds --addSeed levels\level2\level.pak --seedListFile dlc_level2.seed
  ```

  ```
  Bin64vc141\AssetBundlerBatch.exe assetLists --seedListFile dlc_level2.seed --assetListFile dlc_level2_all_v1.assetlist
  ```

  ```
  Bin64vc141\AssetBundlerBatch.exe compare --comparisonType complement --firstAssetFile engine_v1_pc.assetlist --secondAssetFile dlc_level2_all_v1_pc.assetlist
                --output dlc_level2_pruned_v1.assetlist
  ```

  ```
  Bin64vc141\AssetBundlerBatch.exe compare --comparisonType complement --firstAssetFile mygameassets_pruned_v1_pc.assetlist --secondAssetFile dlc_level2_pruned_v1_pc.assetlist --output
                dlc_level2_pruned_v1.assetlist --allowOverwrites
  ```

  The previous command has the `allowOverwrites` option enabled, and it writes to the same pruned list that you created in step 3\.

  ```
  Bin64vc141\AssetBundlerBatch.exe bundles --assetListFile dlc_level2_pruned_v1_pc.assetlist --outputBundlePath dlc_level2_v1.pak
  ```

Don't copy the `.pak` file into the release build yet\. That will be covered in the next part of the tutorial\.

### Simulate Downloading Additional Content<a name="asset-bundler-tutorial-multiple-bundles-simulate-downloading-additional-content"></a>

In this part of the tutorial, you simulate the downloading of additional content by copying the `dlc_level2_v1.pak` asset bundle into your release assets directory\.

**To simulate the downloading of additional content**

1. Run the launcher for the first map \(for example, `AssetBundlingDemoLauncher.exe +map simple`\), and verify that it works\.  
![\[Running the launcher for the first map.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-14.png)

1. Run the launcher for the second map \(for example, `AssetBundlingDemoLauncher.exe +map level2`\)\. The result is a black screen\.  
![\[Running the launcher for the second map with the required bundle missing.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-15.png)

1. Copy the `dlc_level2_v1.pak` asset bundle into your release assets directory\. Your directory should resemble the following image\.  
![\[Copying the dlc_level2_v1.pak asset bundle into the release assets directory.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-16.png)

1. Run the launcher command again for the second map \(`AssetBundlingDemoLauncher.exe +map level2`\)\. The new content displays\.  
![\[Running the launcher for the second map with the required bundle added.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-tutorial-multiple-bundles-17.png)

## Conclusion<a name="asset-bundler-tutorial-multiple-bundles-conclusion"></a>

You now have a working example of a release build of a PC game on Lumberyard that uses multiple asset bundles\. These bundles do not contain duplicate files, and you've performed a workflow that matches how a downloadable content system would add new content to an already released game\.

## Next Steps<a name="asset-bundler-tutorial-multiple-bundles-next-steps"></a>
+ To learn how to use bundles to handle frequent game content updates, see the next tutorial in this series: [Creating Content Patch Bundles with Lumberyard](asset-bundler-tutorial-content-patches.md)\.