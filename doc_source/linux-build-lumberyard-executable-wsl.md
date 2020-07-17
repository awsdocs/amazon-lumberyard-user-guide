# Setting up the Windows Subsystem for Linux to Deploy Your Amazon Lumberyard Linux Executable<a name="linux-build-lumberyard-executable-wsl"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

Microsoft Windows Professional builds 14393\.0 and later provide the Windows Subsystem for Linux \(WSL\), an integrated Linux kernel and bash shell that you can use when developing Amazon Lumberyard games for Linux platforms\. This topic will walk you through the steps to set your Windows 10 development machine up to use it when building your game for Linux\.

Before you start, make sure you are running the 64\-bit version of Windows 10 Professional build 14393\.0 and later\. You can check this by opening a cmd window and running the command **winver** at the prompt\.

1. Enable *Developer Mode* in Windows 10 by going to the *Settings* app, selecting *Updates & Security" > For Developers* and turning on "Developer Mode"\. You may get an installation failure message, but that's okay; Lumberyard only needs the Developer Mode to be enabled, not installed\.

1. Press the Windows key \(or select the Search box from the taskbar\), type "bash", and press Enter\. You will be prompted to install the WSL package from the Microsoft Store\. This step assumes you do not have another bash shell, like Git bash or Cmder installed\. If you do, go to the next step\. If you don't, go to Step 4\.

1. If you have a bash shell installed, you must use the PowerShell to install WSL\.

   Open PowerShell \(PS\) as an Administrator and run the following PS command:

   ```
   C:\>Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
   ```

   If you have any issues with the installation, refer to [Microsoft's WSL installation help guidance here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)\.

1. If you do not have another bash shell installed, you can install WSL from the Microsoft Store\. [Microsoft provides specific guidance here](https://docs.microsoft.com/en-us/windows/wsl/install-win10)\. Choose Ubuntu *18\.X\.X LTS*, not 16\.X\.X\.

   Let the install complete without interruption\.

1. Once the install has completed, reboot your computer\.

1. If the installation was successful, go to the *Start menu* and launch *Bash on Ubunto on Windows*\.

   You will be prompted to create a user\. If it doesn't, open the Windows cmd tool as an Administrator and run the following:

   ```
   C:\>lxrun /setdefaultuser root
   (Open bash)
   $ adduser {your user name} sudo
   (switch back to Admin command prompt)
   C:\>lxrun /setdefaultuser {your user name}
   ```

1. Verify the version of Ubuntu from the bash shell by running the following command:

   ```
   lsb_release -a
   ```

   You should see output like this:

   ```
   No LSB modules are available.
   Distributor ID: Ubuntu
   Description:    Ubuntu 18.04.3 LTS
   Release:        18.04
   Codename:       bionic
   ```

   Confirm that you have installed Ubunto 18\.XX\.X LTS\.

You are now ready to deploy Lumberyard Linux game executables to your local computer\.