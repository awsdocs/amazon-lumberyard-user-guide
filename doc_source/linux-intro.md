# Creating Lumberyard dedicated servers for Linux<a name="linux-intro"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

Lumberyard supports compiling a Windows client for a multiplayer project and connecting to a Linux dedicated server\. You must do the following for the Windows client to work properly on a Linux dedicated server:
+ [Compile the assets on a Windows computer](linux-compile-assets-on-windows.md)
+ [Compile the server executable for use on a Linux computer](linux-build-lumberyard-executable.md)
+ [Compile a Windows client to use to connect to the Linux server](game-build-intro.md)

Once compiled, you can deploy assets to either a Linux server or Windows client\.

**Topics**
+ [Prerequisites](#linux-prerequisites)
+ [Compiling Assets on a Windows Computer](linux-compile-assets-on-windows.md)
+ [Building the Lumberyard Executable for Linux](linux-build-lumberyard-executable.md)
+ [Testing the Windows Client to Linux Server Connection](linux-test-windows-client-linux-server-connection.md)
+ [Preparing the GameLift Package](linux-prepare-gamelift-package.md)
+ [Setting up Ubuntu on Amazon EC2](linux-set-up-ubuntu-amazon-ec2.md)

## Prerequisites<a name="linux-prerequisites"></a>

You must have the following:
+ Lumberyard source code
+ Windows computer with a Lumberyard development environment and the ability to generate a Windows build
+ Linux computer with Ubuntu on Amazon Elastic Compute Cloud \(Amazon EC2\)

  For information, see [Setting up Ubuntu on Amazon EC2](linux-set-up-ubuntu-amazon-ec2.md)\.
+ Familiarity with the following:
  + [Amazon Elastic Compute Cloud \(Amazon EC2\)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
  + [Connect to your Linux instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html)