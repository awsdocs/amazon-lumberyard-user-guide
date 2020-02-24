# Android Support<a name="android-intro"></a>

Follow this guide to create Android applications \(apps\) using Lumberyard\. This guide shows you how to do the following:
+ Configure the build tools to generate assets that your app loads\.
+ Build and debug code\.
+ Generate different types of apps for development or release\.

**Topics**
+ [Prerequisites](#android-prerequisites)
+ [Quick Start: Running the Samples Project on Android Devices](android-quick-start.md)
+ [Anatomy of an Android Application](anatomy-of-apk.md)
+ [Setting Up Your Environment](android-setting-up-environment.md)
+ [Building Your Android Game](building-your-android-game.md)
+ [Using the Virtual File System](using-the-virtual-filing-system-vfs.md)
+ [Running the Deployment Tool](run-the-deployment-tool.md)
+ [Additional Details for Android](additional-details-for-android.md)
+ [PAK Files](pak-files-for-android.md)
+ [Troubleshooting for Android](troubleshoot-android.md)
+ [Using a Samsung Device with Lumberyard](android-samsung-lumberyard.md)
+ [Using the AWS Device Farm for Android Builds](android-builds-aws-device-farm.md)

## Prerequisites<a name="android-prerequisites"></a>

To build games for Android, meet the following requirements:
+ Install Lumberyard on your computer\. You should be familiar with Lumberyard Editor, the Shader Compiler, and Asset Processor\.
+ You're comfortable using a command line interface\.
+ You have built the PC code at least once\.
+ Visual Studio 2017 with the **Mobile development with C\+\+** workload for debugging \(PC only\)
+ An Android SDK supporting API level 29 or later
+ Your device is [configured ](http://developer.android.com/tools/device.html) for development and connected to your computer using a USB cable\.

**Topics**

**About Lumberyard Binaries**  
In this guide, you'll see references about the directory where the Lumberyard binaries are placed\. These binaries are placed either by the installer or as a result of you rebuilding them\. When you install Lumberyard, you'll see the following directories:

**For PC**
+ `dev/Bin64vc141` – Binaries generated with Visual Studio 2017

**For Mac**
+ `dev/BinMac64`

If you use binaries generated with Visual Studio 2017, continue to use the mentioned executable from that directory, such as `Bin64vc141/AssetProcessor.exe`\.