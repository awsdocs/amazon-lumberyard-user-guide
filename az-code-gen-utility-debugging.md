# Debugging the AZ Code Generator Utility<a name="az-code-gen-utility-debugging"></a>


****  

|  | 
| --- |
| AZ Code Generator is in preview release and is subject to change\. | 

When using Waf and the AZ Code Generator utility, you might need to [debug Waf Python scripts](az-code-gen-waf-debugging.md) and your [template drivers](az-cod-gen-template-driver-debugging.md)\. You can also debug the AZ Code Generator utility itself, although it is less likely to be necessary\. You can debug the AZ Code Generator utility by using Visual Studio in Windows or Xcode in macOS\.

**Topics**
+ [Prerequisites](#az-code-gen-utility-debugging-prerequisites)
+ [Debugging the AZ Code Generator Utility from the Waf build](#az-code-gen-utility-debugging-from-waf-build)
+ [Setting Visual Studio Debug Arguments](#az-code-gen-utility-debugging-visual-studio-arguments)
+ [Setting Xcode Debug Arguments](#az-code-gen-utility-debugging-xcode-arguments)

## Prerequisites<a name="az-code-gen-utility-debugging-prerequisites"></a>

 The required preliminary steps depend on your operating system\. 

### Windows Debugging<a name="az-code-gen-utility-debugging-windows"></a>

To debug AZ Code Generator using Visual Studio in Windows, you must generate a Visual Studio HostTools solution \(`.sln`\) file\.

**To generate a Visual Studio HostTools solution file**

1. Enter the following command from the `dev` folder\. 

   ```
   lmbr_waf.bat configure --enabled-game-projects= --specs-to-include-in-project-generation=host_tools --visual-studio-solution-name=HostTools
   ```

1. In Visual Studio, open the `dev/Solutions/HostTools.sln` file\. 

### macOS Debugging<a name="az-code-gen-utility-debugging-osx"></a>

 To enable Waf support for Xcode, perform the following steps to generate an Xcode project\. 

**To generate an Xcode project**

1.  Open the `dev/_WAF_/specs/all.json` file\.

1.  Temporarily add `AzCodeGenerator` to `modules`\. 

1.  Run `./lmbr_waf.sh configure` to regenerate the Xcode project\. 

1.  Open the `dev/Solutions/LumberyardSDK.xcodeproj` file\.

## Debugging the AZ Code Generator Utility from the Waf build<a name="az-code-gen-utility-debugging-from-waf-build"></a>

To debug the AZ Code Generator Utility from the Waf build, you must find the arguments file generated by Waf\.

Waf generates an arguments file that is passed to AZ Code Generator as a command line parameter\. All command line parameters from Waf for AZ Code Generator are contained inside the arguments file\. This file is useful for debugging specific Waf AZ Code Generator invocations\. To make the arguments file that you use available to Waf, add the `--zones=az_code_gen` option to the Waf command line\. 

## Setting Visual Studio Debug Arguments<a name="az-code-gen-utility-debugging-visual-studio-arguments"></a>

To set up debugging of AZ Code Generator from Visual Studio, perform the following steps\.

**To debug AZ Code Generator from Visual Studio**

1. Perform the steps to set up Windows debugging as described in [Prerequisites](#az-code-gen-utility-debugging-prerequisites)\. 

1.  In the **Visual Studio Solution Explorer**, right\-click **AzCodeGenerator**, and then select **Properties**\. 

1.  Under **Debugging**, paste the path to the arguments file into **Command Arguments**\. 

1.  Click **OK** to close the **Property** window\. 

1.  Right\-click **AzCodeGenerator** and then click **Set as StartUp Project**\. 

1.  Press **F5** to launch the debugger\. 

## Setting Xcode Debug Arguments<a name="az-code-gen-utility-debugging-xcode-arguments"></a>

To set up debugging of AZ Code Generator from Xcode, perform the following steps\.

**To debug AZ Code Generator from Xcode**

1.  Perform the steps to set up macOS debugging as described in [Prerequisites](#az-code-gen-utility-debugging-prerequisites)\. 

1.  In Xcode, under the **Product**, **Scheme** menu, choose **AzCodeGenerator**\. 

1.  At the bottom of the **Product**, **Scheme** menu, choose **Edit Scheme**\. 

1.  Under **Arguments, **add a new entry to **Arguments Passed On Launch** that contains your debug arguments\. 

1.  Under **Info**, from the **Executable** drop down, select **Other**\. 

   1.  Navigate to the directory `dev/BinMac64.Debug/azcg/AzCodeGenerator`\. 

   1.  Click **Choose**\. 

1.  **Close** the scheme editor\. 

1.  Choose **Product, Run** to launch the debugger\. 