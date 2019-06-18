# Importing Your Lumberyard Project into Android Studio<a name="android-studio-import-lumberyard-project"></a>

After you create a Lumberyard project, you can import it into Android Studio\.

**To import your Lumberyard project into Android Studio**

1. Open Android Studio\.

1. On the **Welcome to Android Studio** screen, click **Import project \(Eclipse ADT, Gradle, etc\.\)**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

1. Locate the Android Studio project that was created when you ran the `lmbr_waf configure` command\. The default location is `lumberyard_version\dev\Solutions\LumberyardAndroidSDK`\.

1. In the **Gradle Sync** dialog box indicating that Gradle settings are not configured for this project, click **OK**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

1. When the project has been imported and opens, do the following: 
   + Click **Project** to view the project source view pane\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)
   + Click **Build Variants** to view the build targets and change the build configuration for your target project\. This impacts the FeatureTestsLauncher, MultiplayerProjectLauncher, and SamplesProjectLauncher only\. The build configuration for all other targets during the build process is ignored\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)
   + Click **Android Monitor** to view the logcat and system monitors as well as CPU/GPU, memory, and network usage\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)
   + Click **Gradle Console** to view the build output\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)