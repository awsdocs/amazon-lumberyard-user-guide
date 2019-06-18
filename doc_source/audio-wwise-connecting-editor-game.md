# Connecting Wwise to the Editor and Game<a name="audio-wwise-connecting-editor-game"></a>

You can establish a remote connection between Wwise and Lumberyard for your project's debug and profile builds of Lumberyard\. By default, this feature is disabled\. Remote connecting is not supported for performance and release builds\.

**To enable remote connection**

1. In a text editor, create a file in the `lumberyard_version\dev` directory and name it `user.cfg`\.

1. Open the file and enter the following parameter and value: **s\_WwiseEnableCommSystem=1**\.

1. Save the file\.

1. Open your game or Lumberyard Editor\.
**Note**  
If your game or Lumberyard Editor is already running, close and reopen it\.

1. Open the Wwise Authoring Tool and open the Wwise project associated with your game\.

1. In the Wwise Authoring Tool, click **Remote**\.

   The **Remote Connections** dialog displays a list of computers to which you can connect\.

1. Select the `Localhost` entry and click **Connect**\.
**Note**  
`Localhost` is the running instance of the game or Lumberyard Editor on your computer with remote connection enabled\.

1. To verify a successful connection, see the **Profile View** in Wwise\. You can live edit parameters, mute or solo objects or sounds, and tweak effects in the Wwise project\. Because remote connection is engaged, you can hear the changes instantly\. Remote connecting is useful not only for profiling but also for debugging\.