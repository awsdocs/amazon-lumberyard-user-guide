# Creating macOS Games<a name="osx-intro"></a>


****  

|  | 
| --- |
| This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

You can use Lumberyard to build macOS applications\. Lumberyard includes four macOS\-supported sample projects that you can use to learn how to build assets for macOS games using the Asset Processor, build shaders using the remote shader compiler, and build and deploy macOS applications using the Lumberyard build tools\.

**Topics**
+ [Prerequisites](#osx-prerequisites)
+ [Setting Up Your Mac](#osx-setting-up)
+ [Building macOS Games](osx-game-building.md)
+ [Building Game Assets for macOS Games](osx-assets-building.md)
+ [Building Shaders for macOS Games](osx-shaders-building.md)
+ [Running macOS Games](osx-game-deploying.md)
+ [macOS Debugging and Troubleshooting](osx-debugging-troubleshooting.md)
+ [Creating a Project for Your macOS Games](osx-game-creating.md)

## Prerequisites<a name="osx-prerequisites"></a>

To build games for macOS or iOS, Lumberyard requires the following on your Mac: 
+ [Lumberyard Mac Support Files](https://aws.amazon.com/lumberyard/downloads/)
+ [Xcode 10](https://developer.apple.com/xcode/download/) or later
+ OS X El Capitan

**Note**  
Lumberyard Editor requires Windows 7 or later to edit levels\. You must have access to a PC with Lumberyard installed and be able to navigate and run commands from Terminal on your Mac\.

## Setting Up Your Mac<a name="osx-setting-up"></a>

After you download and extract Lumberyard on your Mac, you must run Lumberyard Setup Assistant to install the third\-party software that is required to run the game and compile the game code, engine, and asset pipeline\.

**To run Lumberyard Setup Assistant**

1. Open the directory where you extracted Lumberyard and navigate to the `/dev/Tools/LmbrSetup/Mac` directory\. Run the `SetupAssistant`\.

1. Verify that the engine root path is correct\.

1. On the **Get started** page, select the following and then click **Next**: 
   + **Run your game project**
   + **Compile the game code**
   + **Compile the engine and asset pipeline**
   + **Compile the Lumberyard Editor and tools**
**Note**  
Lumberyard Editor is not supported on macOS\. Selecting this option enables the ability to build the asset processor and resource compiler only\.
   + **Compile for iOS devices**
   + \(Optional\) **Compile for Android devices**
**Note**  
Select this option if you are developing for Android devices\. You must have the Android SDK installed on your Mac\.

1. Follow the instructions onscreen to complete the installations for any third\-party software or SDKs that you need\. For more information about using Lumberyard Setup Assistant, see [Using Lumberyard Setup Assistant to Set Up Your Development Environment](lumberyard-launcher-intro.md)\.

1. Open a command line window and navigate to your Lumberyard `dev` directory\.

1. To initialize the build system, run the following command: `sh lmbr_waf.sh configure`

1. In the Finder, open the `user_settings.options` file \(located in the `/lumberyard/dev/_WAF_/` directory\)\.

1. Verify that **enabled\_game\_projects** is set to your game project\. For example, you can set this option to SamplesProject\. If **enabled\_game\_projects** is not set correctly, edit and save the `user_settings.options` file and then run the `configure` command \(`sh lmbr_waf.sh configure`\) again\.
