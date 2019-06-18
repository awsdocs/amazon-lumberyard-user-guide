# Running Lumberyard Setup Assistant<a name="lumberyard-launcher-using"></a>

Before you run Lumberyard Setup Assistant, verify the following:
+ `3rdParty.txt` file appears in the `lumberyard_version\3rdParty` directory
+ `engineroot.txt` appears in the `lumberyard_version\dev` directory

 Lumberyard Setup Assistant requires these files to properly detect third\-party software and SDKs\.

**To use Lumberyard Setup Assistant**

1. Open Lumberyard Setup Assistant with your preferred method:
   + From the desktop, double\-click the **Setup Assistant** icon
   + Navigate to the `lumberyard_version\dev\Tools\LmbrSetup\Win` directory and double\-click `SetupAssistant.bat`

1. In the **Custom Install** box, click **Customize**\.

1. Verify that the engine root path is correct\.

1. On the **Get started** page, select what you want to do:
   + **Run your game project**
   + **Run the Lumberyard Editor and tools** – Use Lumberyard Editor to create a game
   + **Compile the game code**\* – Compile the game code to include any changes that you have made
   + **Compile the engine and asset pipeline**\* – Compile the engine code and asset pipeline to include any changes that you have made
   + **Compile the Lumberyard Editor and tools**\* – Compile Lumberyard tools to include any changes that you have made
   + **Compile for Android devices\***
   + **Setup for Linux Dedicated Server\***
**Note**  
\*If you select any of these options, additional dependencies might appear in the **Install software** and **Required SDKs** pages\. Follow the instructions in Lumberyard Setup Assistant to obtain the software and third\-party SDKs that aren't installed\.

   You can also create, enable, and disable these capabilities from the command line\. For more information, see [Using Lumberyard Setup Assistant Batch](lumberyard-launcher-batch-using.md) and [Lmbr\.exe](lmbr-exe.md)\.

1. Select **Visual Studio 2015**, **Visual Studio 2017**, or both\. 
**Note**  
To use both versions of Visual Studio, see [Configuring Visual Studio 2015 and 2017 for Lumberyard](#lumberyard-launcher-visual-studio-configuration)\.  
![\[Use Lumberyard Setup Assistant to configure Lumberyard, and install software and plugins.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/lumberyard-launcher.png)
**Note**  
For more information about Visual Studio for Lumberyard, see [Visual Studio](setting-up-system-requirements.md#lumberyard-visual-studio-requirement)\.

1. Click **Next**\.

1. Follow the instructions on each page\.

1. When you have the required software and SDKs installed, click **Configure project** or **Launch Editor**\. For more information about configuring your project, see [Creating Lumberyard Game Projects](configurator-intro.md)\.

1. Log in your existing Amazon account or create an account to use the editor\.

## Configuring Visual Studio 2015 and 2017 for Lumberyard<a name="lumberyard-launcher-visual-studio-configuration"></a>

If you want to use Lumberyard with multiple versions of Visual Studio, you must configure the Lumberyard build system \(Waf\) for each version\. Lumberyard uses Waf and the options that you select in Lumberyard Setup Assistant to generate Visual Studio solutions and to build your game project\. You can find the generated `.sln` files in the `lumberyard_version\dev\Solutions` directory\.

**Note**  
We recommend that only advanced users configure both versions of Visual Studio\.

**To configure the Waf settings for each Visual Studio version**

1. Navigate to the `lumberyard_version\dev\_WAF_` directory\.

1. In a text editor, open the `user_settings.options` file\.

1. Under `[Visual Studio Project Generator]`, set `msvs_version` to **14** for Visual Studio 2015\.

1. At a command\-line prompt, navigate to the `lumberyard_version\dev` directory\.

1. To configure your build, enter the following command\.

   ```
   lmbr_waf configure
   ```

   This generates the Visual Studio solution and build for the version that you specified in the `user_settings.options` file\. The solution file is in the `lumberyard_version\dev\Solutions` directory\.

1. Repeat these steps for Visual Studio 2017\. For step 3, set `msvs_version` to **15**\.