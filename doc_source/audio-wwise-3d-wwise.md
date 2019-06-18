# Upgrading Wwise LTX to Full Version<a name="audio-wwise-3d-wwise"></a>

 See the following procedures to upgrade your Wwise LTX to the full version\. Lumberyard supports Wwise version 2017\.2\.4\.6590 in which these upgrade instructions apply\.

After you upgrade the SDK, project, and soundbanks, you can open your game in Lumberyard to test your sounds\. 

**Topics**
+ [Upgrading the SDK](#audio-wwise-upgrading-sdk)
+ [Upgrading Your Project](#audio-wwise-upgrading-project)
+ [Upgrading Your Soundbanks](#audio-wwise-upgrading-soundbanks)

## Upgrading the SDK<a name="audio-wwise-upgrading-sdk"></a>

**To upgrade the SDK from Wwise LTX to the full version**

1. Open **Wwise Launcher**\. If you don't have it, install it from [https://www.audiokinetic.com/download](https://www.audiokinetic.com/download)\.

1. On the **WWISE** tab, under **Install New Version**, select **Wwise 2017\.2\.4\.6590**\.

1. Click **Install**\.

1. Under **Packages**, select **SDK \(C\+\+\)**\.

1. Under **Deployment Platforms**, select the platforms that you require for your project\.
**Note**  
Some platform components are available only after you purchase them from Audiokinetic\. For more information on licensing, see [https://www.audiokinetic.com/pricing](https://www.audiokinetic.com/pricing)\.

1. Enter the installation directory and click **Next**\.
**Note**  
Take note of this directory, as you will need to navigate there in a later step\.

1. Select the plugins that you want to install, and then click **Install**\.

1. After installation is complete, use a file explorer to navigate to the `lumberyard_version\dev\3rdParty\Wwise` directory\.

1. Create a directory named **`2017.2.4.6590`**\.

1. Navigate to the Wwise installation directory, and then copy the `SDK` directory into `lumberyard_version\dev\3rdParty\Wwise\2017.2.4.6590`\.

1. To verify that Lumberyard recognizes the Wwise installation and configuration:

   1. Run Lumberyard Setup Assistant\.

   1. On the **Install optional SDKs** page, verify that there is a green check mark next to **Audiokinetic Wwise**\.

1. In a file browser, navigate to the `lumberyard_version\dev\Code\CryEngine\CrySoundSystem\implementations\CryAudioImplWwise` directory\. 

1. In a text editor, open the `wscript` file\.

1. Edit the `uselib` parameter to **WWISE** and save the file\.

   This instructs the WAF build system to use Wwise instead of Wwise LTX\.

1. Configure WAF and build the project\. For more information, see [Building Your Game Project](building-your-lumberyard-game-project.md)\.

## Upgrading Your Project<a name="audio-wwise-upgrading-project"></a>

After you have successfully configured and built Lumberyard, you can upgrade your content\. See the following procedure to upgrade an existing Wwise LTX project to use the full version of Wwise\.

**Prerequisites**  
If your Wwise LTX project and soundbanks are under source control, you must check them out\. Check out the entire `lumberyard_version\dev\game_project\Sounds` directory\. After you complete this procedure to upgrade your project, mark for **Add** any new files created by the upgrade process, and then revert any unmodified files before submission\.

**Important**  
During the upgrade process, be sure to read each dialog that Wwise displays\.

**To upgrade your project from Wwise LTX to Wwise Full**

1. Open **Wwise Launcher**\.

1. On the **WWISE** tab, in the **Versions Installed** list, find **2017\.2\.4\.6590**\. Verify that it lists the full version and does not include LTX in the version\.

1. Click **Launch Wwise \(64\-bit\)**\.

1. If this is the first time running Wwise Authoring Tool for this version, an End\-User License Agreement \(EULA\) dialog appears\. Review the EULA and then accept or decline\.

1. In the **Project Launcher** dialog, click **Open Other** and open the `file_name.wproj` file for your game project\. 

   You can find this file in the `lumberyard_version\dev\game_project\Sounds\wwise_project` directory\.

1. If a message appears stating that you are upgrading from a previous version of Wwise, this means that you must upgrade the Wwise project XML schema\. The dialog lists the files to be updated and highlights any files that are read\-only\.

   The message also states that this action is a one way project upgrade, meaning that the upgraded project will no longer load with Wwise LTX\.

   If preferred, make a backup of your Wwise LTX project before you click **Yes** in this dialog\.

1. The **Project Load Log** dialog displays all the changes made\. You may see information about default work units that were missing and were created\. 

   If your Wwise project is under source control, ensure that you add these `.wwu` files to your depot\. 

1. Close the dialog\.

1. Save the Wwise project\.

Wwise LTX uses a single generic platform\. After upgrading to Wwise, you can edit the platforms for your project\.

**To edit your project's platforms**

1. Open your project in Wwise\.

1. Choose **Project**, **Platform Manager**\.

1. Select the platforms you want to include, and then save\.

1. Close and then reopen your project before upgrading your soundbanks in the next section\.

## Upgrading Your Soundbanks<a name="audio-wwise-upgrading-soundbanks"></a>

After you have successfully upgraded the SDK and your project, you can now rebuild your soundbanks\.

**Note**  
Before you rebuild your soundbanks, you must apply the full license\.

**To apply the full license to Wwise**

1. Open your project in Wwise\.

1. Choose **Project**, **License Manager**\.

1. Choose to either import your license or paste it from the clipboard\.

1. Click **Save**\.

**To rebuild your soundbanks**

1. Open the **SoundBank Layout**\. To do this, do one of the following:
   + Press **F7**\.
   + Choose **Layouts**, **Soundbank**\.

1. Select all **SoundBanks**, **Platforms**, and **Languages**\.

1. Click **Generate**\.

   The **Generating SoundBanks** dialog appears and displays the progress\.
**Note**  
The most common errors encountered during the generate process are caused by read\-only files or by not having a license applied to the project\.