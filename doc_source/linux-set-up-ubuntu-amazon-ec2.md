# Setting up Ubuntu on Amazon EC2<a name="linux-set-up-ubuntu-amazon-ec2"></a>

****  
This feature is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\. 

Before you can install the required software to compile Lumberyard on Linux, you must do the following:
+ Set up an Ubuntu Linux virtual machine on Amazon Elastic Compute Cloud \(Amazon EC2\)\. For instructions, see [How to Launch a Linux Virtual Machine](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/) and select Ubuntu 18\.04 LTS\. The Linux virtual machine \(instance\) is launched on Amazon EC2 within the [AWS Free Tier](https://aws.amazon.com/free/)\.
+ Create an archive, if you haven't done so already\. For instructions, see [Compiling Assets on a Windows Computer](linux-compile-assets-on-windows.md)\. Deploy and unpack the archive to your Ubuntu Linux virtual machine by running the following command:

  ```
  tar -xvf YYYY-MM-DD_HH-mm-ss.tar
  ```

**To install required software for Lumberyard on the Ubuntu Linux virtual machine**

1. On your Linux machine, in a terminal, change directory to `MultiplayerSample/dev`\.

1. Install the required software to build Lumberyard by running the following command:

   ```
   sudo sh Tools/LmbrSetup/Linux/setup.sh
   ```