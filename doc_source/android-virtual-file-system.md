# Using Virtual File System with Android<a name="android-virtual-file-system"></a>

The **Asset Processor** can use the virtual file system \(VFS\) to serve files to your Android devices over a USB connection\. This method offers the following benefits: 
+ You can edit game content and data on a PC and view changes on the Android devices\.
+ You needn't rebuild the Android application package \(`.apk`\) file when editing nonvisual data\.
+ You can iterate much faster\.

This topic demonstrates how to set up your PC and Android device to run the Samples Project using VFS\. 

Before you begin setting up VFS, identify the IP address of the PC running the Asset Processor\. You must provide the IP address during setup\.

**To set up VFS**

1. On your PC, edit the `bootstrap.cfg` file \(located in the `lumberyard_version\dev` directory\) to set `remote_filesystem` to **1**\. This notifies the runtime to turn on VFS\.

1. Tell the runtime to create a connection over USB by setting the following: 

   ```
   remote_ip=127.0.0.1
   android_connect_to_remote=1
   wait_for_connect=0
   ```

1. Save your changes and then copy the file to your device using the **Android Debug Bridge** command line window\.
   + If you have a carrier\-locked device, run the following command:

     ```
     adb push bootstrap.cfg /storage/sdcard0/SamplesProject/bootstrap.cfg
     ```
   + If you have an unlocked device, run the following command:

     ```
     adb push bootstrap.cfg /storage/emulated/0/SamplesProject/bootstrap.cfg
     ```
**Note**  
You are responsible for complying with the terms applicable to your Android device, including restrictions on unlocking the Android bootloader\.

1. \(Optional\) To send traffic to the shader compiler through VFS, edit the `system_android_es3.cfg` file \(located in the `lumberyard_version\dev` directory\) to add `r_AssetProcessorShaderCompiler=1`\.

**To enable USB I/O connections to your device**

1. Ensure you have built an `.apk` file so that you can run your game with VFS\. For instructions, see [Building Game Assets for Android Games](android-assets-building.md)\.

1. On your PC, edit the `AssetProcessorPlatformConfig.ini` file \(located in the `lumberyard_version\dev` directory\) to add `es3=enabled` to the `[Platforms]` section\. This enables the **Asset Processor** to create data for Android devices\.

1. Start the **Asset Processor** \(located in the `lumberyard_version\dev\Bin64` directory\)\.

1. Install the game on your device by entering the following in an ADB command line window: `adb install -r BinAndroid.Debug\SamplesProject.apk`

1. Tell your Android device to send traffic to the **Asset Processor** by entering the following in an ADB command line window: `adb reverse tcp:45643 tcp:45643`

**To run the game**
+ Launch your game by tapping the icon on your device's home screen\. You can also launch your game from the Visual Studio 2015 debugger\.
**Note**  
You can check the **Asset Processor** to verify a connection from **PC\-GAME** with **es3**\. Serving files from your PC can affect load time, so it may take time for the game world to appear\.