# Creating Release Builds for PC<a name="game-build-release"></a>

You can create a release build of your game for multiple platforms, including PC, iOS, and Android\.

The following procedures describe how to create release builds for the PC\. For information about creating release builds for Android and iOS, see [Creating Android and iOS Games](mobile-support-intro.md)\.

You can create a formal release build that generates a complete image of your game in a directory that you can deploy that doesn't require Asset Processor or other files\. This image does not change your build or source\. This procedure also requires the built shaders that are generated from a [shader compiler server](mat-shaders-custom-dev-remote-compiler.md) or by using [game mode](lumberyard-editor-menus.md#lumberyard-editor-menus-game) in Lumberyard Editor\. 

**Topics**
+ [Creating a Formal Release Build](#creating-a-formal-release-build)
+ [Running a Build from Visual Studio](#game-build-release-vs)

## Creating a Formal Release Build<a name="creating-a-formal-release-build"></a>

The following describes the three major steps to create a release build:

1. Build the paks\. This creates the root release build directory and generates files required to run your game\.

1. Generate the shader `.pak` files and copy them into your release build directory\.

1. Compile the game and engine in [release](game-build-intro.md) mode\.

**Prerequisites**  
Before you start, build your game project\. See [Building Your Game Project](building-your-lumberyard-game-project.md)\. 

**To create a formal release build**

1. **Create the root release build directory and build the paks**

   Open a command line window and navigate to the `lumberyard_version\dev` directory\. 

1. Enter the following command:

   ```
   BuildSamplesProject_Paks_PC.bat
   ```

   This batch file generates a `\samplesproject_pc_paks` directory that includes the files required to run your game, not including shaders and executables\. You generate these files in a later step\.
**Note**  
If you are not in the Samples Project, edit the file and modify the paths it references\. You can also rename the file if preferred\. The following example shows the part of the `BuildSamplesProject_Paks_PC.bat` that you can customize\. The `/gamefolder=` parameter references the directory name of your project\. The `/game=` parameter specifies the directory name that will be created when you run this batch file\.  

**Example**  

   ```
   ...
   echo ----- Processing Assets Using Asset Processor Batch ----
   .\%BINFOLDER%\AssetProcessorBatch.exe /gamefolder=SamplesProject /platforms=pc
   IF ERRORLEVEL 1 GOTO AssetProcessingFailed
   
   echo ----- Creating Packages ----
   rem lowercase is intentional, since cache folders are lowercase on some platforms
   .\%BINFOLDER%\rc\rc.exe /job=%BINFOLDER%\rc\RCJob_Generic_MakePaks.xml /p=pc /game=samplesproject
   IF ERRORLEVEL 1 GOTO RCFailed
   
   ...
   ```

1. **Build and pack the shaders**

   For more information about generating shaders, see the following:
   + [Remote Shader Compiler](mat-shaders-custom-dev-remote-compiler.md)
   + [Compiling Shaders for Release Builds](asset-pipeline-shader-compilation.md)
   + [Shader Cache and Generation](mat-shaders-custom-dev-cache-intro.md)

   1. To build the shaders, do one of the following:
      + If you run a remote [shader compiler server](mat-shaders-custom-dev-remote-compiler.md), retrieve the shader list file from the server's file system\. This file is typically named `ShaderList_Platform.txt`\. Copy this file to the `lumberyard_version\dev` directory\.
      + If you don't run a remote shader compiler server, open Lumberyard Editor, navigate through the levels that you want to ship while in game mode until all the shaders are generated, and then close Lumberyard Editor\. You can skip this step if all shaders in the level are already generated\.

   1. To pack the shaders, open a command line window and navigate to the `lumberyard_version\dev` directory\. Do one of the following:
      + If you run a remote [shader compiler server](mat-shaders-custom-dev-remote-compiler.md) and copied a shader list in the previous step, enter the following command: 

        ```
        lmbr_pak_shaders.bat ShaderList_Platform.txt
        ```
      + If you generated shaders by navigating the levels in Lumberyard Editor, enter the following command:

        ```
        lmbr_pak_shaders.bat
        ```
**Note**  
If you are not in the Samples Project, customize the `lmbr_pak_shaders.bat` batch file before you run it\. To do this, edit the highlighted parameter in the following example\.  

      ```
      ...
      
      set SOURCESHADERLIST=%1
      set GAMENAME=SamplesProject
      set DESTSHADERFOLDER=Cache\%GAMENAME%\PC\user\Cache\Shaders
      
      ...
      ```

      The batch file output specifies the directory where the packed shaders are located, such as `\Build\pc\SamplesProject`\. 

   1. Copy the resulting `.pak` files to the `samplesproject` directory located in the `samplesproject_pc_packs` directory with the rest of the `.pak` files\.

1. Compile the game and engine and then copy the binaries into the release directory\. To do this:

   1. In a command line window, navigate to the `lumberyard_version\dev` directory\.

   1. Compile your game project in [profile](game-build-intro.md) mode by entering the build command for your version of Visual Studio: 

      ```
      lmbr_waf build_win_x64_vs2015_profile -p all
      ```

      Alternatively, you can use Visual Studio to build `game_and_engine` in release mode\. This builds the actual release version into `Bin64vc140_or_vc141.Release` and copies all required `.dll` files\.

      ```
      lmbr_waf build_win_x64_vs2015_release -p game_and_engine
      ```

      The build creates a `Bin64vc140_or_vc141.Release` directory within `lumberyard_version\dev` and places your game binaries in it\.

      For more information about project configuration parameters \(debug, profile, performance, release\) and build command options, see [Build Configuration](waf-commands.md#build-parameters)\.

   1. Copy the `Bin64vc140_or_vc141.Release` directory to the `samplesproject_pc_paks` directory such that it has its own `Bin64vc140_or_vc141.Release` directory\. Optionally, rename this directory\.

1. If your game does not have a menu system or UI, typically during development stages, then you can use the following instructions to create a batch file that launches a specific level\. 

   1. Create a batch file in the root of your release directory, such as in `samplesproject_pc_paks`\. You can name it anything you like, such as, `LaunchMyLevel.bat`\.

   1. Edit the batch file and enter the following command, customizing as needed:

      ```
      start release_directory\launcher_executable_name +map level_name
      ```

      The following example shows the contents of a `launch.bat` file for launching the Fur Technical Sample within the Samples Project\. In this example, the batch file is placed in the root of the game directory\. Its code navigates to the `Bin64vc140_or_vc141.Release` directory, launches `SamplesProjectLauncher.exe`, and then loads the level `fur_technical_sample`\.  
**Example**  

      ```
      start Bin64vc140.Release\SamplesProjectLauncher +map fur_technical_sample
      ```
**Note**  
If the build does not run, see the `dev.log`, `user.log`, `log.log`, or `game.log` files in the `release_directory\launcher_executable_name\user\log` directory for more information\.

1. \(Optional\) You can create a player login method\. To do this, you can write your own solution or use the provided sample code in the [User Login: Default](gems-system-gem-user-login.md) gem, which is located in the `lumberyard_version\dev\Gems\UserLoginDefault` directory\.

## Running a Build from Visual Studio<a name="game-build-release-vs"></a>

Open the property page of `SamplesProjectWindowsLauncher`\.

Before you can run a release build from Visual Studio, you must change the following debugging properties for the project\. The following example commands specify the Samples Project:
+ Change `Command` to `lumberyard_version\samplesproject_pc_paks\Bin64vc140_or_vc141.release\SamplesProjectLauncher.exe`
+ Change `Command Arguments` to `+map map_name`
+ Change `Working Directory` to `lumberyard_version\samplesproject_pc_paks\Bin64vc140_or_vc141.release`