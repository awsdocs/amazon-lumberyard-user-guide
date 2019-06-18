# Building and Debugging Your Lumberyard Android Application in Android Studio<a name="android-studio-debug-lumberyard-application"></a>

After your Lumberyard project is imported, you can build and debug it using Android Studio\.

**To run and debug your application in Android Studio**

1. In Android Studio, select a game project to debug from the target list in the menu bar\.

   The prepopulated list of targets vary depending on the Android Studio version\.

   The Stable version might display the following: 
   + SamplesProjectLauncher
   + MultiplayerProjectLauncher
   + MultiplayerProjectLauncher\-native
   + SamplesProjectLauncher\-native

   The Canary version might display the following: 
   + SamplesProjectLauncher
   + MultiplayerProjectLauncher

   For Stable versions of Android Studio 2\.1\.x, select the target with the `-native` suffix in order to debug native code\.

1. Set your native break points\.

1. Connect your Android device to your computer\.

1. In Android Studio, click **Debug target**\.

1. In the **Select Deployment Target** dialog box, select your device and click **OK**\.
**Note**  
Lumberyard does not support Android emulators\. If you do not see your physical device, click **Cancel** and run `adb kill-server` in the terminal pane in Android Studio\. Then attempt another run/debug build\.

1. Android Studio will build the project, launch the application, and connect to the debugger\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/android_studio_debugger.png)

1. You can also do the following from the menu bar: 
   + Click **Make project** to build all targets in the project, minus the APK packaging step\.
   + Click **Select target** to run the selected game project \(if multiple game projects are enabled\)\.
   + Click **Run target** to run the selected game project with application\-specific monitoring on the **Android Monitor** tab\.
   + Click **Debug target** to run the selected game project with the Android Studio debugger attached\.