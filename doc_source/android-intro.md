# Android Support<a name="android-intro"></a>

You can use Lumberyard to build your games for Android devices such as the Samsung Galaxy Note 4, LG Nexus 5, and Kindle Fire HDX\. For more information, see [Creating Android and iOS Games](mobile-support-intro.md)\. Lumberyard includes two Android\-supported sample projects that you can use to learn how to build assets for Android, build shaders using the remote shader compiler, and build the Lumberyard runtime using the build tools\.

## Prerequisites<a name="android-prerequisites"></a>

To build games for Android, Lumberyard requires the following: 
+ Visual Studio 2015 with Update 1 or later for debugging \(PC only\)
+ SDK\-19 \(Android 4\.4\.2\) to SDK\-23 \(Android 6\.0\)
+ Your device [set up for development](http://developer.android.com/tools/device.html) and connected to your computer using a USB cable

## Setting Up Your PC<a name="android-setting-up-pc"></a>

After you download and extract Lumberyard on your PC, you must extract and run Lumberyard Setup Assistant to install the third\-party software that is required to run the game and compile the game code, engine and asset pipeline, and for Android devices\.

**To install third\-party software using Lumberyard Setup Assistant**

1. Run Lumberyard Setup Assistant by double\-clicking `SetupAssistant.bat`, which is located in the Lumberyard root directory \(`lumberyard_version\dev`\)\.

1. In Lumberyard Setup Assistant, on the **Get started** page, select **Compile for Android devices** and click **Next**\.

1. Follow the instructions on the screen to complete the installations for any third\-party software or SDKs that you need\. For more information about using Lumberyard Setup Assistant, see [Using Lumberyard Setup Assistant to Set Up Your Development Environment](lumberyard-launcher-intro.md)\.

1. Modify your environment variables by doing the following:

   1. In the Windows **Control Panel**, click **System**, **Advanced system settings**\.

   1. In the **System Properties** dialog box, click **Environment Variables**\.

   1. Under **User variables**, edit the **PATH** variable to add the directory where you installed the Android SDK and the OS\-tools and tools subdirectories\. For example: **C:\\Android\\android\-sdk, C:\\Android\\android\-sdk\\platform\-tools, C:\\Android\\android\-sdk\\tools**

   1. Add the Java SDK and JRE to the **PATH** variable\. For example: **C:\\Program Files\\Java\\jdk1\.7\.0\_79\\bin and C:\\Program Files\\Java\\jre7\\bin**

1. Locate the directory where you installed the Android SDK\. Run the **SDK Manager** and select the version of the SDK that you want to install\. You must also install a version of the build tools\. Note the version you installed\.

1. Modify configuration files to tell Lumberyard which version of the SDK to use when building your game:

   1. In the File Explorer, locate `\_WAF_\android` in the directory where you installed Lumberyard\.

   1. Edit the `android_settings.json` file to set `BUILD_TOOLS_VER` with the version of the build tools that you just installed and to set `SDK_VERSION` with the version of the SDK that you want to use\.

   1. Save the file\.

1. In a command line window, change to the `lumberyard_version\dev` directory\.

1. To initialize the build system, run the following command:

   ```
   lmbr_waf.bat configure
   ```

## Setting Up Your Mac<a name="android-setting-up-mac"></a>

After you download and extract Lumberyard on your Mac, you must extract and run Lumberyard Setup Assistant to install the third\-party software that is required to run the game and compile the game code, engine and asset pipeline, and that is required for Android devices\.

**To install third\-party software from Lumberyard Setup Assistant**

1. Unzip the `SetupAssistant.zip` file \(located in the `lumberyard_version/Tools/LmbrSetup/Mac` directory\) and move the `.APP` into `Bin64`\. Run Lumberyard Setup Assistant\.

1. In Lumberyard Setup Assistant, on the **Get started** page, select **Run your game project**, **Compile the game code**, and **Compile for Android devices**\. Click **Next**\.

1. Follow the instructions on the screen to complete the installations for any third\-party software or SDKs that you need\. Be sure to install the Wwise audio library and JDK v7u79\. For more information about using Lumberyard Setup Assistant, see [Using Lumberyard Setup Assistant to Set Up Your Development Environment](lumberyard-launcher-intro.md)\.

1. In a command line window, change to the `lumberyard_version/dev` directory\.

1. To initialize the build system, run the following command:

   ```
   sh lmbr_waf.sh configure
   ```

1. In the Finder, open the `user_settings.options` file \(located in the `/lumberyard/dev/_WAF_/` directory\)\.

1. Edit the `bootstrap_tool_param` as follows:

   ```
   bootstrap_tool_param = --none --enablecapability compilegame --enablecapability compileandroid  --no-modify-environment
   ```

1. Modify your environment variables by doing the following:

   1. If you are using Bash, edit the `.bash_profile` file to add the paths for `android-sdk/platform-tools` and `android-sdk/tools`\.

   1. In a command line window, change to the SDK directory and run the following command: `tools/android update sdk --no-ui`

1. Locate the directory where you installed the Android SDK\. Run the **android** executable file \(located in the `tools` directory\) and select the version of the SDK that you want to install\. You must also install a version of the build tools\. Note the version you installed\.

1. Modify configuration files to tell Lumberyard which version of the SDK to use when building your game:

   1. In the File Explorer, locate `/_WAF_/android` in the directory where you installed Lumberyard\.

   1. Edit the `android_settings.json` file to set `BUILD_TOOLS_VER` with the version of the build tools that you just installed and to set `SDK_VERSION` with the version of the SDK that you want to use\.

   1. Save the file\.
**Important**  
You must save these files with the correct line endings\. If you are not using the Vim text editor, please research the correct method to save your files\. If you are using Vim, save the file by running the following command: `w ++ff=mac`

1. In a command line window, change to the `lumberyard_version/dev` directory\.

1. To initialize the build system, run the following command:

   ```
   sh lmbr_waf.sh configure
   ```

**Topics**
+ [Prerequisites](#android-prerequisites)
+ [Setting Up Your PC](#android-setting-up-pc)
+ [Setting Up Your Mac](#android-setting-up-mac)
+ [Configuring Your Game Project for Android](android-game-configuring.md)
+ [Building Android Games](android-game-building.md)
+ [Building Game Assets for Android Games](android-assets-building.md)
+ [Building Shaders for Android Games](android-shaders-building.md)
+ [Android Debugging](android-debugging.md)
+ [Deploying Android Games](android-game-deploying.md)
+ [Running Android Games](android-game-running.md)
+ [Using Virtual File System with Android](android-virtual-file-system.md)
+ [Using a Samsung Device with Lumberyard](android-samsung-lumberyard.md)
+ [Using Lumberyard with Android Studio](android-studio-lumberyard-intro.md)
+ [Using the AWS Device Farm for Android Builds](android-builds-aws-device-farm.md)