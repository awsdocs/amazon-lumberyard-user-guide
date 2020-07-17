# Preparing the GameLift Package<a name="linux-prepare-gamelift-package"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

Lumberyard supports compiling and deploying the Windows client for a multiplayer project on a Linux dedicated server\. You must have completed the following:
+ [Compiled the assets on a Windows computer](linux-compile-assets-on-windows.md)\.
+ [Built the Lumberyard executable for use on a Linux computer](linux-build-lumberyard-executable.md)\.
+ [Tested the connection between the Windows client and the Linux server](linux-test-windows-client-linux-server-connection.md)\.

Once you have tested the client and server connection, you can prepare your GameLift package, which allows you to use Amazon GameLift to deploy your game servers\. 

**To prepare the GameLift package**

1. On your Linux computer, in a terminal console window, run the following command: `./MultiplayerSample_CreateGameLiftPackage.sh`

1. In the AWS CLI, enter the following to upload your package to Amazon GameLift:

   ```
   aws gamelift upload-build --operating-system AMAZON_LINUX --build-root "./GameLiftPackageLinux" --name "your package name" --build-version "your build version" --region us-west-2
   ```
**Note**  
If you do not have the AWS CLI installed, enter the following in the command line window:  

   ```
   sudo pip install awscli
   sudo pip install --upgrade awscli
   ```