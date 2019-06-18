# Building Shaders for Android Games<a name="android-shaders-building"></a>

Lumberyard uses a versatile shader system to achieve high quality, realistic graphics\. Because the shader compilation pipeline depends on the Windows\-specific HLSL optimizer, you must connect to a shader compiler on your PC when running a game on an Android device during the development stage\. This compiles the subset of shaders required by your game on demand\.

**Note**  
You must connect your PC and Android device to the same network and configure any firewalls to allow traffic through port 61453\.

When a new shader is compiled, the game waits for the binary shader permutation to compile on your PC and be sent back to your device\. Once this occurs, the shader is cached on your device until you delete the game\. When you are ready to release your game, you must pack up and include all cached binary shaders\.

You can use a whitelist to specify the IP addresses that are allowed to connect to your remote shader compiler\. 

For information, see [Creating a Whitelist for the Remote Shader Compiler](mat-shaders-custom-dev-remote-compiler.md#mat-shaders-custom-dev-remote-compiler-whitelist)\.

## Building the Shader Compiler<a name="android-shaders-building-compiler"></a>

Building Lumberyard Editor will also build the shader compiler\. Otherwise, you can build the shader compiler by changing to the `lumberyard_version\dev` directory in a command line window and enter the following command for your version of Visual Studio:

```
lmbr_waf build_win_x64_vs2015_profile -p all --targets=CrySCompileServer
```

The shader compiler executable is created in the `lumberyard_version\dev\Tools\CrySCompileServer\x64\profile` directory\.

You must also set up the mobile device system CFG file \(`system_android_es3.cfg`\) to connect to the remote shader compiler on the PC\.

## Running the Shader Compiler<a name="android-shaders-running-compiler"></a>

You can run the shader compiler on your PC\.

**To run the shader compiler on your PC**

1. Navigate to the `lumberyard_version\dev` directory\.

1. Edit the `system_android_es3.cfg` file to set the `localhost` for `r_ShaderCompilerServer` to the IP address of the PC on which you will run the shader compiler\.

1. Navigate to the `lumberyard_version\dev\Tools\CrySCompileServer\x64\profile` directory\.

1. Double\-click the `CrySCompileServer.exe` file\.

## Generating Shaders<a name="android-shaders-generate"></a>

You can generate shaders for your Android game\.

**To generate shaders**

1. Build, deploy, and run your game on an Android device\. For information, see [Building Android Games](android-game-building.md)

1. In your game, explore every area in every level to ensure that all shader permutations required for the game are generated\. Exit the game when you are finished\.

## Building Shader \.Pak Files<a name="android-shaders-build-pak-files"></a>

The shaders pak is automatically generated and deployed when building on release\. If you want to manually build the file, you can open a command line window and batch file to build a `.pak` file that includes your shaders\.

**To build a shader \.pak file**

1. Run the **Remote Shader Compiler**\. For more information, see [Remote Shader Compiler](mat-shaders-custom-dev-remote-compiler.md)\. 

1. In a command line window, navigate to the `dev` directory of your build and locate the `lmbr_pak_shaders.bat` file\. For macOS, the file has the `.sh` extension\.

1. To use the `lmbr_pak_shaders.bat` file, enter a command that provides the name of the game project for which to build the shaders as an argument: 

   ```
   lmbr_pak_shaders.bat game_project_name GLES3 es3
   ```

   For example, to build the shaders for the Samples Project, enter the following command:

   ```
   lmbr_pak_shaders.bat SamplesProject GLES3 es3
   ```

## Deploying Shader \.Pak Files<a name="android-shaders-deploy-pak-files"></a>

When the batch file finishes building the shader PAK file for your game project, you will find the following in the `lumberyard_version\dev\Build\es3\game_project_name\` directory: 
+ `ShaderCache.pak` – Contains all compiled shaders that are used only when the shader cannot be found in the current level's shader cache\.
+ `ShaderCacheStartup.pak` – Contains a subset of compiled shaders that are used to accelerate the startup time of the engine\.

**To enable your game to run the shaders from the PAK files**

1. Copy the `shaders*.pak` files to the `lumberyard_version\dev\Cache\game_project_name\es3\user` directory\.

1. When the shader PAK files are in the correct cache location, you can deploy the assets to the device\. The game will use the shaders and will only connect to the remote shader compiler if it can't find a shader\.