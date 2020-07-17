# Compiling Assets on a Windows Computer<a name="linux-compile-assets-on-windows"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

You must compile assets and the `3rdParty` directory for the multiplayer project on a Windows computer\. Once compiled, you can deploy assets to either a Linux server or Windows client\.

**To compile assets on a Windows computer**

1. Run the Project Configurator \(located in the `\lumberyard_version\dev\Bin64` directory\)\.

1. In the Project Configurator, select **MultiplayerProject** and click **Set as default**\.

1. Close the Project Configurator\.

1. Edit the `bootstrap.cfg` file \(located in the `\dev` directory\) to set `connect_to_remote` to **0**\.

1. Run the following command from the `\dev` directory: `lmbr_waf.bat configure`

1. Follow these instructions for [Build and bundle assets for release in Lumberyard](asset-bundler-tutorial-release.md)\. Alternatively, you can run the `BuildMultiplayerSample_Paks_PC_dedicated.bat` file \(located in the `\dev` directory\)\.

1. To create a Linux deployment package, run the `MultiplayerSample_LinuxPacker.bat` file \(located in the `\dev` directory\) as Administrator\.

**Note**  
Deployment archives are created in the `\dev\unix_archives` directory and uniquely named based on the creation time\.

**Tip**  
If you plan to deploy over a slow network connection, you can use the `--compress` option to create a smaller archive\.

**To deploy files to a Linux computer**  
Use your preferred file transfer tool to deploy the `YYYY-MM-DD_HH-mm-ss.tar` file on your Windows computer to your Linux computer\. For more information, see [Connect to Your Linux Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
You do not need to deploy files to a Linux computer if you use the same computer to compile and to deploy files\.