# Deploying Android Games<a name="android-game-deploying"></a>

Before you can deploy your game to Android devices, you must ensure the shader compiler \(located in the `lumberyard_version\dev\Tools\CrySCompileServer\x64\profile\CrySCompileServer.exe` directory\) is running on your PC\. For more information, see [Building Shaders for Android Games](android-shaders-building.md)\.

You can deploy your game to Android devices using the Remote Console\.

Once you have deployed your game, see [Running Android Games](android-game-running.md)\.

## Using the Remote Console to Deploy Your Android Game<a name="android-game-deploying-remote-console"></a>

You can operate and configure the Lumberyard runtime application using a series of console commands on your PC\. You must connect your PC and Android device to the same network and configure any firewalls to allow traffic through port 4600\.

**To deploy your game using the Remote Console**

1. Launch the **Remote Console** application \(located in the `lumberyard_version\dev\Tools\RemoteConsole\` directory\)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

1. On the **Full Log** tab, view the output from the runtime engine's logging system\.

1. Start running a Lumberyard application on your Android device\.

1. In the Remote Console, click **Targets** and then enter the IP address of the Android device for **Custom IP**\.

1. \(Optional\) If your network allows you to assign IP addresses per device so that the IP address is always fixed to a MAC address, you can edit the `params.xml` file \(located in the same directory as the application\) to add your device to the list of targets: 

   ```
   <Targets>
        <Target name="PC" ip="localhost" port="4600"/>
        <Target name="Android" ip="192.168.5.247" port ="4600"/>
   </Targets>
   ```

   Adding your device to the targets allows you to select from a list of devices instead of entering the IP address each time\.

1. Verify that you see a green connected status in the Remote Console, which indicates the Remote Console can successfully connect to your Lumberyard application\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

1. Issue commands to your application by entering in the text window\. The text window supports autocomplete, and commands like `map` will detect the available options\. Useful commands include: 
   + `cl_DisableHUDText` – Disables the heads\-up display text\.
   + `g_debug_stats` – Enables debugging for gameplay events\.
   + `r_DisplayInfo` – Displays rendering information\.
   + `r_ProfileShaders` – Displays profiling information for the shaders\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)