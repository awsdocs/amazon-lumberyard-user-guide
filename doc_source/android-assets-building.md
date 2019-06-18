# Building Game Assets for Android Games<a name="android-assets-building"></a>

When you build an Android game using Lumberyard, you must first build the assets that are included with the game\. All built assets are located in the `cache` directory of your Lumberyard installation\. For example, when you build the Samples Project, the assets are saved to the `lumberyard_version\dev\cache\SamplesProject\es3` directory\. The initial build of the Samples Project assets may take up to an hour to process, but incremental changes should process almost instantly\.

**To build Android game assets on your PC**

1. Close all instances of Lumberyard Editor and the Asset Processor\.

1. Edit the `bootstrap.cfg` file \(located in the `lumberyard_version\dev` directory\) to set `sys_game_folder` to **SamplesProject** \(or the project you want to build\)\. Save the file\.

1. Edit the `AssetProcessorPlatformConfig.ini` file \(located in the `lumberyard_version\dev` directory\) to uncomment `es3=enabled`\. Save the file\.
**Note**  
If the Asset Processor was running when you edited the `AssetProcessorPlatformConfig.ini` file, you must restart the Asset Processor\. 

1. Open Lumberyard Editor, which automatically launches the Asset Processor to process and build your game assets as you make changes to your game levels in Lumberyard Editor\.
**Note**  
You can also launch the Asset Processor \(GUI or batch version\) from the `lumberyard_version\dev\Bin64` directory\.

## Using Assets in Your Game<a name="android-assets-using"></a>

You can use assets in your game by copying them to your device manually or by packing them into an `.apk` file\. We recommend copying the assets to your device manually for a faster build time during development\.

### Manually Copying Assets<a name="android-assets-using-manual-copy"></a>

As part of the build process, Lumberyard can automatically copy assets built by the Asset Processor to your device, or you can manually copy assets from a command line window using Android Debug Bridge \(ADB\)\. Game assets should be copied to the `/storage/sdcard0/Your_Game_Name` directory\. 

For example, to manually copy the Samples Project assets, enter the following in a command line window:

```
adb push cache/SamplesProject/es3 /storage/sdcard0/SamplesProject
```

### Building Assets into an \.Apk File<a name="android-assets-using-build-apk"></a>

To build an `.apk` file that includes all of your assets, edit the `project.json` file for your game project and set `place_assets_in_apk` to **1**\. This method requires a longer build time than manually copying your assets\.

For example, to build an `.apk` file for the Samples Project assets, edit the `project.json` file \(located in the `lumberyard_version\dev\SamplesProject` directory\) to set `place_assets_in_apk` to **1**: 

```
    "android_settings": {
        "package_name"  : "com.lumberyard.samples",
        "version_number": 1,
        "version_name"  : "1.0.0.0",
        "orientation"   : "landscape",
        "place_assets_in_apk" : 1
    },
```

When you generate a build, your computer creates an `.apk` file that includes an executable and game data\. Be sure to run the shader compiler when you run your game for the first time\.

**Note**  
If you receive an error indicating the `lumberyard_version\dev\Solutions\android\SamplesProject\assets` directory does not exist, you can try running the command from a command line window with Administrator privileges\.

## Sharing Game Assets Between PCs and Macs<a name="android-assets-sharing"></a>

After you build the assets to include with your Android game, you can share the `cache` folder between your PC and Mac\. This ensures that changes you make in Lumberyard Editor on your PC are automatically retrieved by macOS\.

**To set up asset sharing on your PC**

1. Navigate to the `\dev` folder in the directory where you installed Lumberyard\.

1. Right\-click the `cache` folder and click **Properties**\.

1. In the **cache Properties** dialog box, on the **Sharing** tab, click **Advanced Sharing**\. You must have administrator privileges\.

1. In the **Advanced Sharing** dialog box, select **Share this folder**\. Click **OK**\.

1. \(Optional\) Click **Permissions** to set permissions for specific users\. This step is required if you want to modify the shared assets on your Mac\.

**To view shared assets on your Mac**

1. In the Finder, click **Go**, **Connect to Server**\.

1. For the **Server Address**, enter **smb://*IP address or DNS name of PC*/Cache**

1. Click **Connect**\.

1. \(Optional\) Configure your system preferences to automatically connect to the shared folder when macOS starts:

   1. Open **System Preferences**, **Users & Groups**, **Login Items**\.

   1. In the **Login Items** dialog box, click **\+** to add a new login\.

   1. In the **Shared** pane, locate and select your PC\. In the right pane, select your shared `cache` folder and click **Add**\.

1. In a Terminal window, navigate to the `\dev` folder in the directory where you installed Lumberyard\.

1. To create a symbolic link to the shared `cache` folder, run the following command: `sudo ln –s /Volumes/Cache Cache`

   If prompted, enter the password for your macOS login\.