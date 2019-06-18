# Android Debugging<a name="android-debugging"></a>

You can debug your Android game using Visual Studio 2015\.

**To debug your Android game**

1. In the Visual Studio 2015 installer, select **Cross platform tools for C\+\+ development**\. Follow the on\-screen instructions to complete the installation\.

1. In Visual Studio 2015, click **Tools**, **Options**\.

1. In the left pane of the **Options** dialog box, expand **Cross Platform**, **C\+\+**, and click **Android**\.

1. Edit the paths to use the correct directories on your computer:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/android-debugging.png)

1. Click **OK** and close Visual Studio 2015\.

1. Build a debug version of an `.apk` file and then relaunch Visual Studio 2015\.
**Note**  
Before you can use Visual Studio 2015 to run and debug the `.apk`, you must build your game assets for Android and then deploy them to the device or bundle them with the `.apk`\. For information, see [Building Game Assets for Android Games](android-assets-building.md)\.

1. In Visual Studio 2015, click **File**, **Open Project/Solution**\. Locate and select your `.apk` file \(`BinAndroid.Debug\`\)\.

1. In the project window, right\-click the project and click **Properties**\.

1. Do one of the following:
   + If you are using Visual Studio 2015 without any updates, enter **\.CryEngineActivity** for **Launch Activity**\.
   + If you are using Visual Studio 2015 with Update 1 or later, verify that the correct activity is already set for **Launch Activity**\. For the Samples Project, you should see **LAUNCHER activity \(com\.lumberyard\.samples\.SamplesProjectActivity\)**\. 

1. For **Additional Symbol Search Paths**, enter **dev/Code** and **dev/BinAndroid\.Debug**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/android-debugging-launch-activity.png)

1. Open your code files by pressing **Ctrl\+O** or clicking **File**, **Open**\.

1. Set breakpoints, if necessary, and then press **F5** to run your game\.