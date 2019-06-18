# Building the Lumberyard Executable for Linux<a name="linux-build-lumberyard-executable"></a>


****  

|  | 
| --- |
| This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

After compiling the assets on a Windows computer, you must build the Lumberyard executable for a Linux computer\.

**To build the Lumberyard executable for Linux**

1. Open a command line window on your Linux computer and enter the following command to unpack the deployed archive:

   ```
   tar -xvf YYYY-MM-DD_HH-mm-ss.tar
   ```

1. Enter the following command to navigate to the `MultiplayerSample/dev` directory:

   ```
   cd ~/MultiplayerSample/dev
   ```

1. \(Optional\) Enter the following command to verify that you are using the supported versions of the dependencies:

   ```
   sudo sh Tools/LmbrSetup/Linux/setup.sh
   ```

1. Enter the following command to configure your environment:

   ```
   sh lmbr_waf.sh configure --3rdpartypath absolute_path_to_3rdParty folder --bootstrap-tool-param "--enablecapability compileengine --enablecapability compilegame" --update-settings True
   ```  
**Example command for Multiplayer Sample**  

   ```
   sh lmbr_waf.sh configure --3rdpartypath ~/MultiplayerSample/3rdParty/ --bootstrap-tool-param "--enablecapability compileengine --enablecapability compilegame" --update-settings True
   ```

1. Edit the `system_linux_pc.cfg` file to set `log_RemoteConsoleAllowedAddresses` to your IP address\. The file is located in the `lumberyard_version/dev/MultiplayerSample_pc_Paks_Dedicated` directory\.

1. Enter the following command to build other builder assistant tool binaries\. This is required only if you are using a non\-release build\.

   ```
   sh lmbr_waf.sh build_linux_x64_profile -p host_tools
   ```

1. Enter the following command to build the Lumberyard executable for Linux:

   ```
   sh lmbr_waf.sh build_linux_x64_profile_dedicated -p game_and_engine
   ```

   The executable appears in the `BinLinux64.Dedicated` directory\.

**Note**  
To build debug or release targets, replace *profile* with **debug** or **release** in the same commands\.  

```
sh lmbr_waf.sh build_linux_x64_debug -p host_tools
sh lmbr_waf.sh build_linux_x64_debug_dedicated -p game_and_engine
```
The executable appears in the `BinLinux64.Debug` directory\.  

```
sh lmbr_waf.sh build_linux_x64_release -p host_tools
sh lmbr_waf.sh build_linux_x64_release_dedicated -p game_and_engine
```
The executable appears in the `BinLinux64.Release` directory\.