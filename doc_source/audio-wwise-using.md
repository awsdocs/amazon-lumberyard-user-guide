# Audiokinetic Wwise LTX<a name="audio-wwise-using"></a>

Lumberyard includes Audiokinetic Wwise LTX, which is an exclusive, free version of the Audiokinetic Wwise audio middleware\. Sound designers and composers can use Wwise LTX to work independently from the engineering team and author rich soundscapes for your games\.

If your game requires advanced features, you can upgrade to the full version of Wwise\. For more information, see [Upgrading Wwise LTX to the Full Version](audio-wwise-3d-wwise.md)\.

**Topics**
+ [Installing Wwise LTX Authoring Tool](#audio-installing-wwise)
+ [Running the Wwise LTX Authoring Tool](#audio-setting-wwise-authoring-tool)
+ [Accessing Wwise LTX Documentation](#audio-wwise-using-documentation)

## Installing Wwise LTX Authoring Tool<a name="audio-installing-wwise"></a>

To author sounds with Wwise LTX for your game, you must first install Wwise LTX Authoring Tool\.

**To install Audiokinetic Wwise LTX Authoring Tool**

1. Run [Lumberyard Setup Assistant](lumberyard-launcher-using.md)\.

1. Click **Install software**\.

1. For the **Audiokinetic Wwise LTX Authoring Tool** entry, click **Install it**\. This installs the Wwise Launcher and runs it\.

1. If prompted to sign in to your Audiokinetic account, provide the requested information and click **Sign In**, or click **Skip sign in**\.

1. Select the desired installation components and settings for Wwise LTX or accept the default, and then click **Install**\.
**Note**  
The Wwise LTX SDK is already included in Lumberyard's `3rdParty` directory\. If you prefer a lightweight install, you can clear the SDK component and all the platforms\.

1. If prompted with license terms, review the end user license agreement and then click **Accept**\.

1. Once the installation successfully completes, close the **Wwise Launcher** and return to Lumberyard Setup Assistant\. It should now show that Wwise LTX is installed\.

## Running the Wwise LTX Authoring Tool<a name="audio-setting-wwise-authoring-tool"></a>

To run the Wwise LTX Authoring Tool, you must first open or create a project\. The Samples Project and Starter Game both include a Wwise LTX audio project that you can use\.

**To run the Wwise LTX Authoring Tool**

1. Run **Wwise Launcher**\.

1. Click the **Wwise** tab, then in the Wwise LTX installation, click **Launch Wwise \(64\-bit\)**\. If preferred, click the wrench icon to create a desktop shortcut for later use\.

1. If this is your first time running Wwise LTX, you are prompted again to review and accept the End\-User License Agreement \(EULA\)\. After accepting the EULA, click **Open Other**\.

1. Browse to the `.wproj` file located in `lumberyard_version\dev\project_name\Sounds\wwise_project` directory and click **Open**\.

1. Alternatively, if you are not using the Samples Project or the Starter Game project, you can click **New** to create a Wwise LTX project\. 

   For more information about setting up Wwise for your game project, see [Setting up a Wwise Project](audio-wwise-project-setting-up.md)\.

## Accessing Wwise LTX Documentation<a name="audio-wwise-using-documentation"></a>

You can access the Wwise LTX documentation in the Wwise Authoring Tool\.

**To access Wwise LTX documentation**

1. Open the **Wwise LTX Authoring Tool**\.

1. Do one of the following
   + Press **F1**\.
   + Choose **Help**, **Wwise Help**\.