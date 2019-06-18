# Running Android Games<a name="android-game-running"></a>

Before you can run your game on Android devices, you must deploy your game using the Remote Console\. For information, see [Deploying Android Games](android-game-deploying.md)\.

To run the game on release, certain read\-only console variables must load during runtime in order for the mobile environment to configure properly\. By default, read\-only console variables cannot be modified when running on release\. You must modify this behavior by editing the `IConsole.h` file \(located in the `\dev\Code\CryEngine\CryCommon` directory\) to set the define `ALLOW_CONST_CVAR_MODIFICATIONS` \(line 39\) to **1**\.

**To run your game on an Android device**

1. Launch your game by tapping the icon on your device's home screen\. You can also launch your game from the Visual Studio 2015 debugger\.
**Note**  
You can check the Asset Processor to verify a connection from **PC\-GAME** with **es3**\. Serving files from your PC may impact load time, so it may take time for the game world to appear\.

1. \(Optional\) Load different levels by editing the `SamplesProject\autoexec.cfg` file and running the game again\. Android supports the Advanced\_RinLocomotion level\.

1. Use the following controls to navigate around your game:
   + Switch between cameras by selecting the buttons in the lower right corner of the screen\.
   + Move Rin in the Character Controller view by touching the left side of the screen\.
   + Look around the Character Controller view by touching the right side of the screen\.
   + Jump in the Character Controller view by double\-tapping anywhere on the screen\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/advanced-rin-locomotion-mobile.JPG)

1. \(Optional\) In a command line window, enter `adb logcat` to view logging information for your game\.