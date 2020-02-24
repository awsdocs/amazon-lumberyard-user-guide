# Step 2: Define the basic directory structure for your release<a name="asset-bundler-starter-game-tutorial-step2"></a>

Define the basic directory structure for your release build of the StarterGame\.

1. Create a directory for your release build\. As a best practice, don't make it a subdirectory under your engine root\. Create this release directory outside of your development directory to more readily verify that your release build is release content only, and not development content\.

1. Create a subdirectory under this directory for your build, which includes the release binaries and executables\. In the screenshot shown in step 3 in this procedure, it is named "Release\."

1. Create a peer subdirectory for the game's content with the name of `startergame`\.

   Your directory structure should look like the following:  
![\[The directory structure for the final release bundle for StarterGame.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-folder-structure.png)

1. Copy the release build that you created earlier in this tutorial into the build subdirectory \(named "Release" in the previous screenshot\) of your release\. These files are the binaries used to run the StarterGame, They are located in `{Lumberyard Install Root Directory here}\dev\Bin64vc141.Release\` \. \(Example: `C:\Amazon\Lumberyard\1.23.0\dev\Bin64vc141.Release\`\)\. Specifically, copy the qtlibs directory\. If this was an actual game release, you'd remove any build\-time artifacts, such as the `.pdb` files\.

   **Note** 

   "Bin64vc141" specifies a Visual Studio 2017 build\. Replace this in the path above with the correct Visual C\+\+ binary version if you are using a different version of Visual Studio\.  
![\[The final release build files before asset bundling.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-release-build-binaries.png)

## Next Step<a name="asset-bundler-starter-game-tutorial-step2.1"></a>

 [Step 3: Build the shader assets](asset-bundler-starter-game-tutorial-step3.md) 