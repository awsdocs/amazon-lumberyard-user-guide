# Building Android Games<a name="android-game-building"></a>

Before you can deploy your game to Android devices, you must ensure the following:
+ The shader compiler \(located in the `lumberyard_version\dev\Tools\CrySCompileServer\x64\profile\CrySCompileServer.exe` directory\) is running on your PC\. For information, see [Building Shaders for Android Games](android-shaders-building.md)\. 
+ You are using Android NDK r11 or above\. For information, see [Android Support](android-intro.md)\.

**Contents**
+ [Building Android Games Using the Lumberyard Editor Deployment Tool Plugin](#android-game-building-deployment-tool)
  + [Setting Deployment Tool Options](#android-game-building-deployment-tool-options)
+ [Building Android Games Using Clang](#android-game-building-clang)

## Building Android Games Using the Lumberyard Editor Deployment Tool Plugin<a name="android-game-building-deployment-tool"></a>

Lumberyard Editor includes a plugin that allows you to build and deploy Android applications\.

**Important**  
If you change your default project, you must ensure the new default project is set for the `enabled_game_project` parameter in the `user_settings.options` file\. You can find this file in the `lumberyard_version\dev\_WAF_` directory\. In a command line window, run the `lmbr_waf.bat configure` command before you start Lumberyard Editor and the **Deployment Tool**\. This command processes and creates the appropriate files for your project\.

**To build and deploy your game for Android using the Deployment Tool**

1. In Lumberyard Editor, choose **File**, **Project Settings**, **Deployment Tool**\.

1. In the **Base Options**, for **Target Platform**, choose **Android ARMv8**
   
1. For **Build Game**, select this option if your game project meets one of the following:
   + You haven't built your game project for the Android target that you specified\.
   + There are code changes to your game project since the last build\.

1. \(Optional\) In the **Asset Options**, for **Mode**, specify how the **Deployment Tool** should deploy the assets for the game:
   + **Local Files** – Loose compiled assets are copied to Android devices after the executable file is installed\. This allows the game to run faster\. If you select this option, you can't enable hot reloading of assets\.
   + **Use Virtual File System** – Assets remain on the PC and the game retrieves the assets at runtime as needed\. This option allows assets that support hot reloading to update automatically in the game if changes are detected on the PC\.

1. Click **Deploy** to build and deploy the game to the Android device, start the [remote shader compiler](mat-shaders-custom-dev-remote-compiler.md), and then launch the game on the Android device\. You can view the progress in the **Deploy Output** console\.

1. \(Optional\) After your initial deployment, if you plan to change art and level assets only, you can decrease the deployment time with the following:

   1. In the **Base Options**, clear the **Build Game** check box\.

   1. In the **Platform Options**, clear the **Clean Device** check box\.

      When you clear these options, the **Deployment Tool** won't build or install the executable, which is only required if you make code changes for your game project\.
**Note**  
If you add new gems to your game project, you must select the **Build Game** check box in order to include the features of those gems\.

### Setting Deployment Tool Options<a name="android-game-building-deployment-tool-options"></a>

The **Deployment Tool** provides the following options that you can set to build and deploy your game\.

![\[Deploy your game project to an Android device with the Deployment Tool.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/android-deployment-tool-options.png)


****  

| Base Options | Description | 
| --- | --- | 
| Target Platform |  Target hardware platform to which to deploy\. You can choose the following options: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/android-game-building.html)  | 
| Build Configuration |  Type of build to send to the device\. You can choose the following options: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/android-game-building.html)  | 
| Target Device |  Local device to which to deploy the build\. This list is auto generated from connected devices\. If devices are not found, **No Devices Connected** is the only entry in the drop\-down menu\.  | 
| Device IP Address |  IP address of the target device\. You can specify an IP address to connect the device for remote logs and whitelist the device to connect to Asset Processor and the shader compiler\.  \[Android only\] If you specify the localhost, this will automatically configure port forwarding for the respective connections\.   | 
| Build Game |  Generates a new build for the **Target Platform** before deployment\.  | 
| Local Current Level |  Toggles between the normal game startup and starting from the currently open level in Lumberyard Editor\. This option is ignored if a level is not loaded in Lumberyard Editor\.  | 


****  

| Asset Options | Description | 
| --- | --- | 
| Mode |  Specifies how files should be deployed to the target device\. You can choose the following options: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/android-game-building.html)  | 
| Asset Processor IP Address |  Specifies the address used for VFS connections when Asset Processor handles shader compiler requests\. This list is auto generated based on the available network adapters\.  \[Android only\] If you specify the localhost, this will automatically configure port forwarding for the respective connections\.   | 
| Shader Compiler |  You can choose the following options: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/android-game-building.html)  | 


****  

| Platform Options | Description | 
| --- | --- | 
|  **Clean Device**  |  Uninstalls the game project from the target device before deployment\. Deployment time will increase\. If you made changes to game content, the executable will be reinstalled each time\.  | 


****  

| Console | Description | 
| --- | --- | 
|  **Deploy Output**  |  Displays the deployment process, including errors\.  | 
|  **Remote Output**  |  Once the deployment process successfully launches the application, the device runtime logs appear\. At the bottom of the **Deployment Tool**, the **Remote Log Status** shows which device, if any, is currently receiving runtime logs\.  | 

## Building Android Games Using Clang<a name="android-game-building-clang"></a>

You can build your game for Android using Clang\. Building for Android \(ARM\) in Visual Studio will build using Clang\.

**To build your game for Android using Clang \(recommended\)**

1. Ensure you are using Android SDK 21 or later and Android NDK r11 or later\. For information, see [Android Support](android-intro.md)\.

1. In a command line window, navigate to your `lumberyard_version\dev` directory\.

1. Build various targets of your game: 

**To build debug**
   + On a PC, run the following command: 

     ```
     lmbr_waf.bat build_android_armv8_clang_debug -p all
     ```
   + On a Mac, run the following command: 

     ```
     sh lmbr_waf.sh build_android_armv8_clang_debug
     ```

**To build profile**
   + On a PC, run the following command: 

     ```
     lmbr_waf.bat build_android_armv8_clang_profile -p all
     ```
   + On a Mac, run the following command: 

     ```
     sh lmbr_waf.sh build_android_armv8_clang_profile -p all
     ```

**To build release**
   + On a PC, run the following command: 

     ```
     lmbr_waf.bat build_android_armv8_clang_release -p all
     ```
   + On a Mac, run the following command: 

     ```
     sh lmbr_waf.sh build_android_armv8_clang_release -p all
     ```

1. Debug your application\. For information, see [Android Debugging](android-debugging.md)\.
