# Testing the Windows Client to Linux Server Connection<a name="linux-test-windows-client-linux-server-connection"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

Lumberyard supports compiling and deploying the Windows client for a multiplayer project on a Linux dedicated server\. You must have completed the following:
+ [Compiled the assets on a Windows computer](linux-compile-assets-on-windows.md)\.
+ [Built the Lumberyard executable for use on a Linux computer](linux-build-lumberyard-executable.md)\.

Once the Lumberyard executable is ready, you can test the connection between the Windows client and the Linux server\.

**To test the client and server connection**

1. Start the Linux server:

   1. In a terminal window, change directory to the `BinLinux64.Dedicated` directory\.

      ```
      $ cd BinLinux64.Dedicated
      ```

   1. The launcher requires that the current working directory contain the data and `multiplayergame` directory, which includes the `.pak` files\. Copy the assets from the `MultiplayerSample_pc_Paks_Dedicated` directory to the `BinLinux64.Dedicated` directory\.

      ```
      $ cp -r ../MultiplayerSample_pc_Paks_Dedicated/* ./
      ```

   1. Run the `MultiplayerSampleLauncher_Server`:

      ```
      $ ./MultiplayerSampleLauncher_Server
      ```

1. Start the remote console on your Windows computer:

   1. Run the `RemoteConsole.exe` file \(located in the `lumberyard_version\dev\Tools\RemoteConsole` directory\)\.

   1. In the **Targets** window, for the **Custom Ip**, enter the server's IP address\.

   1. For the **Custom Port**, enter the server's port\.

      The Linux server echoes the chosen port, which appears in the last line, for example, *Remote console listening on: 4600*\. The server also echoes when the remote console is attached\. If you restart the server, the remote console is automatically reattached\.

   1. In the command line window, run the following command:

      ```
      mphost
      map multiplayersample
      ```

1. Start the Windows client:

   1. Edit the `bootstrap.cfg` file \(located in the `lumberyard_version\dev` directory\) to set `connect_to_remote` to **1**\.

   1. Double\-click the `MultiplayerSampleLauncher.exe` file in the following directory:
      + For Visual Studio 2017: `lumberyard_version\dev\Bin64vc141\`
      + For Visual Studio 2019: `lumberyard_version\dev\Bin64vc142\`

   1. After the launcher loads, open the console by pressing the accent grave key **`** and enter the following command: 

      ```
      mpjoin server_IP_address
      ```