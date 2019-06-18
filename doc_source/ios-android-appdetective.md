# Using AppDetective to Test Your Game Build on the AWS Device Farm<a name="ios-android-appdetective"></a>

Lumberyard provides a script called **AppDetective** that you can use to deploy your game builds to the AWS Device Farm\. This allows you to test your game on numerous devices without having to set up and manage your own hardware\. For example, the Samsung Galaxy S7 uses different graphics processors depending on the sales region\. Rather than acquiring all of the variations for each model that you want to test, you can use the **AppDetective** to deploy to these devices on the AWS Device Farm\. You can access the **AppDetective** script in the `\dev\Tools\AppDetective` directory\.

Testing your game build using the AppDetective and AWS Device Farm requires the following steps:

1. Determine which devices you want to test on\.

1. Configure your game build to test on these devices in the AWS Device Farm\.

1. Use the AppDetective to check the status of the run\.

1. Download your game build artifacts\.

**Topics**
+ [Prerequisites](#ios-android-appdetective-prerequisites)
+ [Setting Your Test Devices](#ios-android-appdetective-determine-test-devices)
+ [Configuring and Testing Your Game](#ios-android-appdetective-configure-game-build)
+ [Checking the Run Status](#ios-android-appdetective-check-run-status)
+ [Downloading Your Game Build Artifacts](#ios-android-appdetective-download-build-artifacts)
+ [AppDetective Command Line Parameters](#ios-android-appdetective-commands)

## Prerequisites<a name="ios-android-appdetective-prerequisites"></a>

To use the **AppDetective** to test your build, you must have the following installed:
+ AWS command line tools

  For information and installation steps, see [AWS Command Line Interface](https://aws.amazon.com/cli/)\.
+ Python modules

  In a command line window, enter the following to install the required Python modules:

  ```
  python -m pip install boto3
  python -m pip install requests
  python -m pip install grequests
  ```

  For information, see [pip 9\.0\.1](https://pypi.python.org/pypi/pip)\.

## Setting Your Test Devices<a name="ios-android-appdetective-determine-test-devices"></a>

The `test_specs.json` file \(located in the `\dev\Tools\AppDetective` directory\) contains a list of the devices on which you can run and test your game\. You can edit this file to modify the list of devices\.

**To set the devices on which to test your game**

1. Navigate to the `\dev\Tools\AppDetective` directory and open the `test_specs.json` file\.

1. Verify or edit the devices that are listed under `device_filter`\. This list determines the devices that are selected for the test\.

   For example, to use Sony Xperia Z4 devices with Android OS version 5 or 6, edit the `device_filter` section as follows:

   ```
   { 
   	"android_fuzz_test": { 
   		"platform": "android", 
   		"appType": "ANDROID_APP", 
   		"device_filter": { 
   			"os_list": ["6", "5"], 
   			"name_list": ["xperia z4"] 
   		}
   ```

1. Test your filter by entering the following in a command line window:

   `C:\> python appDetective.py -tf -tn android_fuzz_test`

1. Verify that the output displays the device name that you specified under `device_filter`\.

   For example, the output for the `device_filter` with `"os_list": ["6", "5"] and "name_list": ["xperia z4"]` should appear as follows:

   `Name: [Sony Xperia Z4 Tablet] OS Version: [5.0.2]`

   Alternatively, if you had specified **S7** for the `name_list`, the output should appear as follows:

   ```
   Name: [Samsung Galaxy S7 Edge (AT&T)] OS Version: [6.0.1] 
   Name: [Samsung Galaxy S7 SM-G930F] OS Version: [6.0.1] 
   Name: [Samsung Galaxy S7 (AT&T)] OS Version: [6.0.1] 
   Name: [Samsung Galaxy S7 (T-Mobile)] OS Version: [6.0.1] 
   Name: [Samsung Galaxy S7 Edge (T-Mobile)] OS Version: [6.0.1] 
   Name: [Samsung Galaxy S7 Edge SM-G935F] OS Version: [6.0.1]
   ```

## Configuring and Testing Your Game<a name="ios-android-appdetective-configure-game-build"></a>

Before you can test your game on the AWS Device Farm, you must configure your game build to include required assets in the executable file\.

**To configure and test your game**

1. Include your game assets in the executable file:

   1. For iOS games, no action is required\.

   1. For Android games, do the following:

      1. Edit the `project.json` file for your game to set `place_assets_in_apk` to **1**\.

      1. Build and pack the shaders into your game, or run the shader compiler on an Amazon EC2 instance for the devices in the AWS Device Farm to compile the shaders\. For information, see [Running the Shader Compiler on Amazon EC2](ios-android-running-shader-compiler-amazon-EC2.md)\.

1. In a command line window, run the following command:

   ```
   python appDetective.py -tn [name of the test spec from the test_specs.json file] -a [game name] -n [project name in the AWS Device Farm] -s
   ```

   For example, if your test spec name is `android_fuzz_test`, your game name is `SamplesProject.apk`, and your project name is `DFTestTutorial`, run the following command:

   ```
   python appDetective.py -tn android_fuzz_test -a SamplesProject.apk -n DFTestTutorial -s
   ```

1. Verify that the output displays the following, with your specified values:

   ```
   Created project DFTestTutorial with ARN:arn:aws:devicefarm:us-west-
   2:330708257384:project:625319c8-b78c-400e-86a6-7ee1f5fab7ee
   
   Creating device pool with the following devices:
   Samsung Galaxy S7 Edge (AT&T)
   Samsung Galaxy S7 SM-G930F
   Samsung Galaxy S7 (AT&T)
   Samsung Galaxy S7 (T-Mobile)
   Samsung Galaxy S7 Edge (T-Mobile)
   Samsung Galaxy S7 Edge SM-G935F
   
   Created Device Pool with ARN:arn:aws:devicefarm:us-west-
   2:330708257384:devicepool:625319c8-b78c-400e-86a6-7ee1f5fab7ee/7a24d8c3-5cbd-4c69-
   afaf-de6e3be6ec02
   Sending data...
   Sending data...
   Sending data...
   Sending data...
   Sending data...
   
   Upload complete
   Started run on Device Farm...
   ```

1. Allow the build to run and complete\. By default, the run will complete in 10 minutes \(600 seconds\)\. You can override the run time by setting the `-d` command and specifying a time, in seconds, in a command line window\.

## Checking the Run Status<a name="ios-android-appdetective-check-run-status"></a>

You can use the AppDetective to check the status at any time during a run\. Do the following to check the run status\.

In a command line window, run the following command:

```
python appDetective.py -tn [name of the test spec from the test_specs.json file] -n [project name in the AWS Device Farm] -g
```

For example, if your test spec name is `android_fuzz_test` and your project name is `DFTestTutorial`, run the following command:

```
python appDetective.py -tn android_fuzz_test -n DFTestTutorial -g
```

## Downloading Your Game Build Artifacts<a name="ios-android-appdetective-download-build-artifacts"></a>

When your game has finished running on the devices in the AWS Device Farm, you can download the artifacts that were generated during the run\. These artifacts include screenshots, videos, and logs\. Do the following to download your game build artifacts\.

In a command line window, run the following command:

```
python appDetective.py -tn [name of the test spec from the test_specs.json file] -n [project name in the AWS Device Farm] -f
```

For example, if your test spec name is `android_fuzz_test` and your project name is `DFTestTutorial`, run the following command:

```
python appDetective.py -tn android_fuzz_test -n DFTestTutorial -f
```

The downloaded files are saved to a directory with the name of your project in the AWS Device Farm\. In this example, the directory is called `DFTestTutorial`\.

## AppDetective Command Line Parameters<a name="ios-android-appdetective-commands"></a>

The AppDetective uses the following command line parameters\.

**`--help`**  
Displays all of the available parameters\.  
Shortcut: `-h`

**`--verbose`**  
Displays a verbose output from the AppDetective and its modules\. This may help to debug any issues with running the AppDetective\.  
Shortcut: `-v`

**`--startrun`**  
Immediately runs your game on the AWS Device Farm\.  
Shortcut: `-s`

**`--repeatrun`**  
Restarts a run with the currently uploaded game\. The `--projectname` parameter is required with this command\.  
Shortcut: `-r`

**`--runduration`**  
Time, in seconds, that the game should run on each device\. The `--projectname` parameter is required with this command\.  
Shortcut: `-d`

**`--getrunstatus`**  
Returns the current state of the run\. The `--projectname` parameter is required with this command\.  
Shortcut: `-g`

**`--fetchartifacts`**  
Retrieves all artifacts—such as log files, screenshots, and videos—for every device in the current run\. The `--projectname` parameter is required with this command\.  
Shortcut: `-f`

**`--fetchartifactsbyjob`**  
Retrieves all artifacts—such as log files, screenshots, and videos—for every device in the specified job\. A job is a specific task issued to the AWS Device Farm and can be found with the `--listjobs` parameter\. The `--projectname` parameter is required with this command\.  
Shortcut: `-fj`

**`--updateapp`**  
Uploads a new version of your game to the current project\. The `--projectname` parameter is required with this command\.  
Shortcut: `-u`

**`--listjobs`**  
Lists the jobs that are currently running on the AWS Device Farm\. You can use this information and the `--fetchartifactsbyjob` parameter to retrieve artifacts for a specific device\. The `--projectname` parameter is required with this command\.  
Shortcut: `-l`

**`--testfilter`**  
Tests the `test_specs.json` file filter and outputs the devices that will be used for the specified settings\.  
Shortcut: `-tf`

**`--deleteallprojects`**  
Deletes all projects and related files and data from the AWS Device Farm\. This action cannot be undone\.  
Shortcut: `-x`

**`--projectname`**  
Name of the project on the AWS Device Farm\.  
Shortcut: `-n`

**`--app`**  
The APK or IPA for your project that you want to upload and run on the AWS Device Farm\.  
Shortcut: `-a`

**`--test_name`**  
The specific test that you want to use from the `test_specs.json` file\.  
Shortcut: `-tn`