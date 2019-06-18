# Configuring Your Game Project for Android<a name="android-game-configuring"></a>

Before you use Lumberyard to build your Android games, you must configure your game project to be built for Android\. You can also customize the Android settings in your game project to allow for store deployment\.

## Prerequisites<a name="android-game-configuring-prerequisites"></a>

To configure your game project for Android, you must have the following: 
+ Lumberyard and the Lumberyard SDK installed
+ Your development environment set up
+ Basic knowledge of the Lumberyard Waf build system and the JSON data format
+ Lumberyard configured to build Android games

  For information, see [Android Support](android-intro.md)\.
+ A game project

## Setting Your Game Project to Build for Android<a name="android-game-configuring-project"></a>

You can enable your game project to be built for Android by modifying certain settings in your game project's `project.json` file\.

**To modify your game project's `project.json` file**

1. In a file browser, navigate to your game project's asset directory\. For example, `\dev\SamplesProject` in the directory where you installed Lumberyard\.

1. Use a text editor to open the `project.json` file\.

1. Verify the following entry appears or add the entry if it does not exist: `"android_settings": {}`

1. Save the `project.json` file\.

1. In a command line window, navigate to the root of the directory where you installed Lumberyard \(`lumberyard_version\dev`\)\.

1. Run the `lmbr_waf configure` command: 
   + On a PC, run the following command: `lmbr_waf.bat configure`
   + On a Mac, run the following command: `./lmbr_waf.sh configure`

   If an error occurs while configuring your game project for Android, a warning message similar to the following is displayed:

   ```
   [WARN] Android settings not found in SamplesProject/project.json, skipping.
   ```

1. You can view the contents of the generated Android project in the Android Studio project directory\. For example, `lumberyard_version\dev\Solutions\LumberyardAndroidSDK\SamplesProjectLauncher`\. 

1. Build and test your game project on Android\. For information, see [Building Android Games](android-game-building.md)\.

## Customizing Android Settings for Your Game Project<a name="android-game-customizing-android-settings"></a>

After you add the Android configuration entry for your game project, you can customize various settings to generate your project and prepare your Android game for store deployment\.

You can customize the following Android settings: 

**Android package name**  
Description: Used for generating the project specific Java activity class and in the AndroidManifest\.xml  
Tag name: `"package_name"`  
Type: String in dot\-separated format  
Example: `"com.mycompany.mygame"`

**Manifest code version number**  
Description: Internal application version number\. Used to set the `android:versionCode` tag in `AndroidManifest.xml`\.  
Tag name: `"version_number"`  
Type: Whole number value  
Default: `1`

**Manifest version name**  
Human readable version number\. Used to set the `android: versionName` tag in `AndroidManifest.xml`\.  
Tag name: `"version_name"`  
Type: String  
Example: "1\.0\.0"

**Orientation**  
Description: Orientation of the Android application\. Used to set the `android:screenOrientation` tag in `AndroidManifest.xml`\.  
Tag name: `"orientation"`  
Type: String  
Valid values: See the [Android Developers](https://developer.android.com/guide/topics/manifest/activity-element.html#screen) page for valid values\.  
Default: "landscape"

**Application icon overrides**  
Tag name: `"icons"`  
Type: Mapping of strings for each resolution option\. All entries require a path relative to `\Code\project\Resources` or an absolute resource path\. Include the name of a `.png` image in the string\.  
Valid values: `"mdpi"`, `"hdpi"`, `"xhdpi"`, `"xxhdpi"`, `"xxxhdpi"`, `"default"` \(the image set for `"default"` is used if a specific DPI override is not specified\)

**Application splash screen overrides**  
Tag name: `"splash_screen"`  
Type: Mapping of two maps   
+ Landscape tag name: `"land"`
+ Portrait tag name: `"port"`
Both orientation maps allow the same options\. All entries require a path relative to `\Code\project\Resources` or an absolute resource path\. Include the name of a `.png` image in the string\.  
Valid values: `"mdpi"`, `"hdpi"`, `"xhdpi"`, `"xxhdpi"`, `"default"` \(the image set for `"default"` is used if a specific DPI override is not specified\)

**Allow assets to pack into the APK**  
Description: Forces the assets to be packed in the APK in non\-release builds  
Tag name: `"place_assets_in_apk"`  
Type: Whole number value  
Valid values: `0` \(No\) or `1` \(Yes\)  
Default: `0`

**Google Play application license key**  
Description: Application license key provided by Google Play\. Required for using APK Expansion files or other Google Play Services\.  
Tag name: `"app_public_key"`  
Type: String \(Base64\-encoded RSA public key\)  
Default value: `"NoKey"`

**Application specific salt value for \(un\)obfuscation when using APK Expansion files**  
Tag name: `"app_obfuscator_salt"`  
Type: String containing a series of random bytes  
Default value: `""`

**Specify whether to use Main APK Expansion**  
Description: Toggles APK Expansion file mode in release builds\.  
Tag name: `"use_main_obb"`  
Type: String value containing either `"true"` or `"false"`  
Default Value: `"false"`

**Specify whether to use the "Patch" APK Expansion file**  
Description: Toggles APK Expansion file mode in release builds\.  
Tag name: `"use_patch_obb"`  
Type: String value containing either `"true"` or `"false"`  
Default Value: `"false"`

**Force APK Expansion file mode in non\-release builds**  
Tag name: `"enable_obb_in_dev"`  
Type: String value containing either `"true"` or `"false"`  
Default Value: `"false"`

**Enable or disable the screen wake lock**  
Description: Toggles whether device will go to sleep while the application is running\.  
Tag name: `"enable_keep_screen_on"`  
Type: String value containing either `"true"` or `"false"`  
Default Value: `"false"`

**RC job override for generating the normal PAK files used in release builds**  
Tag name: `"rc_pak_job"`  
Type: String containing the XML file name relative to `\dev\Bin64\rc`  
o Default Value: `"RcJob_Generic_MakePaks.xml"`

**RC job override for generating the APK Expansion file\(s\)**  
Tag name: `"rc_obb_job"`  
Type: String containing the XML file name relative to `\dev\Bin64\rc`  
Default Value: `"RCJob_Generic_Android_MakeObb.xml"`

**To add an Android setting override**

1. In a file browser, navigate to your game project's asset directory\.

1. Use a text editor to open the `project.json` file\.

1. Add any of the customizable settings above to the `"android_settings"` entry in the `project.json` file\. 

   The following example includes all of the customizable Android settings: 

   ```
   "android_settings" : 
   {
       "package_name"   : "com.lumberyard.samples",
       "version_number" : 1,
       "version_name"   : "1.0.0.0",
       "orientation"    : "landscape",
       "icons"          : 
       {
           "default"    : "AndroidLauncher/icon-xhdpi.png",
   
           "mdpi"       : "AndroidLauncher/icon-mdpi.png",
           "hdpi"       : "AndroidLauncher/icon-hdpi.png",
           "xhdpi"      : "AndroidLauncher/icon-xhdpi.png",
           "xxhdpi"     : "AndroidLauncher/icon-xxhdpi.png",
           "xxxhdpi"    : "AndroidLauncher/icon-xxxhdpi.png"
       },
       "splash_screen"  : 
       {
           "land" :
           {
               "default"    : "AndroidLauncher/splash-xhdpi.png",
   
               "mdpi"       : "AndroidLauncher/icon-mdpi.png",
               "hdpi"       : "AndroidLauncher/icon-hdpi.png",
               "xhdpi"      : "AndroidLauncher/icon-xhdpi.png",
               "xxhdpi"     : "AndroidLauncher/icon-xxhdpi.png"
           },
           "port": 
           {
               "default"    : "AndroidLauncher/icon-xhdpi.png",
   
               "mdpi"       : "AndroidLauncher/icon-mdpi.png",
               "hdpi"       : "AndroidLauncher/icon-hdpi.png",
               "xhdpi"      : "AndroidLauncher/icon-xhdpi.png",
               "xxhdpi"     : "AndroidLauncher/icon-xxhdpi.png"
           }
       }
       "place_assets_in_apk" : 0,
   
       "app_public_key" :
   
           "MIIBIjANBgkqhkiG9w0BALuMbErYaRdAMIIBCgKCAQEAjvkl+K7rVA
           SNkLExAmPlEoWwsxCX1vx7uV3IIH5CQIZBRGT8KeYr6ThWlIPhSMKMIm
           j7KxjdYcil8J0rwrVL3cmAYdMM+02ntnBEemGvRVOKxkDaFc5Fw6tJVv
           3SJ6UyjVtehB7tJupaYdfFe9SVhW0xJZu2YsZLuMbErYaRdrrgXU2Upr
           547mxuyEHJ7jG7YFVrQgxou1W/71QnExAmPlExi6mlsUJBFN4xADikNW
           ZDlI70iHF6ZYyOspZCbVZ9DScN+D5oS3KeY/KKd5WOU6BB8NmTY5VZVd
           UOd4VPRXrYMnRY7FjZJMPujLNvlrAJs5H/G+0wUTR4SI61AiGJiQIDAQ
           AB",
   
           "app_obfuscator_salt" : "8d87473f5b24852836d0652abbd9e9b9869c208",    
           "use_main_obb" : "true",    
           "use_patch_obb" : "false",
           "enable_obb_in_dev" : "false",
           "enable_keep_screen_on" : "true",
           "rc_pak_job" : "RcJob_MakeCustomPaks.xml",
           "rc_obb_job" : "RcJob_MakeCustomAndroidObb.xml"
   },
   ```

1. Save the file\.

1. In a command line window, navigate to the root of the directory where you installed Lumberyard \(`lumberyard_version\dev`\)\.

1. Run the `lmbr_waf configure` command: 
   + On a PC, run the following command: `lmbr_waf.bat configure`
   + On a Mac, run the following command: `./lmbr_waf.sh configure`