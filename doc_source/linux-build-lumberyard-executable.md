# Building the Lumberyard Executable for Linux<a name="linux-build-lumberyard-executable"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

After compiling the assets on a Windows computer, you must build the Lumberyard executable for a Linux computer\. Your Linux executable and compiled game assets must be packaged as the tar archive format \(\.tar\) for transfer to a Linux environment\. To create a Linux deployment package, run the **MultiplayerSample\_LinuxPacker\.bat** file \(located in the **\\dev** directory\) as Administrator\.

When you create the TAR file with the MultiplayerSample\_LinuxPacker\.bat script, it will be given a name based on the current date and time\. While you can name it what you like, keeping the format below is also a best practice, especially if you may be managing multiple packaged versions of your game on the Linux machine\. These instructions assume the following format:

```
YYYY-MM-DD_HH-MM-SS.tar
```

**Copy your TAR file to a Linux platform for deployment**

You will need a Linux environment to complete these steps\. You can create a Linux VM or install a Linux distro on a separate machine, or create a VM on your desktop or in the cloud\. For this guidance, we assume you are using the Ubuntu Linux distro, version 18\.04 LTS or later\. \(AWS' Elastic Compute Cloud VM service provides this as the standard Linux AMI\. [Read more about it here](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/)\.\)

If you are running Windows 10 Professional build 14393\.0 or later, you can use the Windows Subsystem for Linux \(WSL\)\. [Read more about setting it up for the deployment of your Lumberyard game executable here](linux-build-lumberyard-executable-wsl.md)\.

1. Once you have a Linux machine or WSL running, connect to it\. From the shell, run the following command to verify the version:

   ```
   lsb_release -a
   ```

   The output must indicate a version of Ubuntu that is 18\.04 or later, such as:

   ```
   No LSB modules are available.
   Distributor ID: Ubuntu
   Description:    Ubuntu 18.04.3 LTS
   Release:        18.04
   Codename:       bionic
   ```

1. Copy the tarball you created on your Windows machine to a location on the Linux machine\. You can use WinSCP, FTP, or other methods to copy the TAR archive over\. If you are running Linux on a local partition, mount it and copy the files over directly\. If you are using Windows Subsystem for Linux, you can skip to Step 2\.

**To build the Lumberyard executable for Linux**

1. Once you have copied the \.tar file to the Linux machine, open a command line window on your Linux computer \(or use bash if you are running Linux on your local computer\), change to the directory where you placed it, and enter the following command to unpack it:

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