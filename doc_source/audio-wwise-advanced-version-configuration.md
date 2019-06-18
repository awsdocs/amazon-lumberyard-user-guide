# Using a Different Wwise Version<a name="audio-wwise-advanced-version-configuration"></a>

Lumberyard officially supports Wwise version 2017\.2\.4\.6590, but you can use an older or newer version\. Lumberyard is backwards compatible with the 2016 versions of Wwise\. Lumberyard no longer supports versions 2015 and earlier\.

**Note**  
Audiokinetic frequently releases new versions of Wwise, which you can use at your own risk\. Newer versions may be compatible with the current version supported by Lumberyard without requiring major code changes\. However, minor revisions can contain API updates that require code changes in Lumberyard\. Major revisions can require code changes and deeper migration\.

## Configuring an Older Version of Wwise for Lumberyard<a name="specify-an-older-version-of-wwise-for-lumberyard"></a>

**To configure Lumberyard for an older version of Wwise**

1. In a file explorer, navigate to the `lumberyard_version\dev\Code\CryEngine\CrySoundSystem\implementations\CryAudioImplWwise` directory\.

1. In a text editor, open the `wscript_wwise2016.readme.txt` file\.

1. Follow the instructions in that file\. The following is an overview of the procedure contained in that file:

   1. Download a 2016 version of Wwise\.

   1. Copy the `Wwise_version\SDK` directory from the Wwise install directory to the `lumberyard_version\3rdParty\Wwise` directory\.

   1. Open `lumberyard_version\dev\SetupAssistantConfig.json` and modify the version of Wwise in the file\.

      This configures Lumberyard Setup Assistant to look for that particular version instead\.

   1. Replace the `wscript` file in `lumberyard_version\dev\Code\CryEngine\CrySoundSystem\implementations\CryAudioImplWwise` with the Wwise 2016 version of the same file\.

   1. Add a `.json` file that defines the Wwise 2016 SDK for WAF\.

1. After you complete these steps, run Lumberyard Setup Assistant and `lmbr_waf configure` to check for errors\. 

   If no errors occur, build Lumberyard Editor and Engine for Wwise 2016\.

## Configuring a Newer Version of Wwise for Lumberyard<a name="specify-a-newer-version-of-wwise-for-lumberyard"></a>

**To configure Lumberyard for a newer version of Wwise**

1. Download the newer version of Wwise that you want to use\.

1. Copy the `Wwise_version\SDK` directory from the Wwise install directory to the `lumberyard_version\3rdParty` directory\.

1. Open `lumberyard_version\dev\SetupAssistantConfig.json` and replace all occurrences of **2017\.2\.4\.6590** with the newer version that you downloaded\.

   This configures Lumberyard Setup Assistant to look for that particular version instead\.
**Note**  
`SetupAssistantConfig.json` contains a section for **Wwise** and a separate section for **Wwise LTX**\. Modify only the **Wwise** section\.

1. Save and close `SetupAssistantConfig.json`\.

1. Run or refresh Lumberyard Setup Assistant and view the **Install optional SDKs** page\.

1. Verify that the displayed version of Wwise matches the version that you configured\.
**Note**  
The setup instructions in the description still mention Wwise 2017\.2\.4\.6590 because that text is compiled into Lumberyard Setup Assistant\.

1. Complete the steps listed in [Upgrading Wwise LTX to Full Version](audio-wwise-3d-wwise.md)\.