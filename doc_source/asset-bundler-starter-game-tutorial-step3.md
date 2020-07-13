# Step 3: Build the shader assets<a name="asset-bundler-starter-game-tutorial-step3"></a>

Build and add the shader assets for the StarterGame and add them to your release build bundle\.

1. If your remote shader compile server is running \(see Prerequisites at the beginning of this tutorial\), obtain the shader list \(called shaderlist\.txt\) from it\. Otherwise, you must generate one by opening Lumberyard Editor, moving the camera around the initial StarterGame level until you've generated all the shaders locally\. When you're finished, close the editor\.

1. Open a command prompt, navigate to `{Lumberyard Install Root Directory here}\dev\Tools\CrySCompileServer\x64\profile`, and run `CrySCompileServer.exe`\. This will start the local shader server process\. **Do not close the command prompt\.**

1. Open a new command prompt and run `lmbr_pak_shaders.bat StarterGame D3D11 pc`\.

1. When the previous step completes, the shader server has generated `.pak` files for your shaders\. The path is provided in the output of the command\. Copy these files to into your `startergame` directory\.  
![\[The StarterGame release build directory with shader .pak files added.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/assetbundler/asset-bundler-qs-shader-paks.png)

## Next Step<a name="asset-bundler-starter-game-tutorial-step3.1"></a>

 [Step 4: Generate auxiliary data](asset-bundler-starter-game-tutorial-step4.md) 
