# System Requirements<a name="setting-up-system-requirements"></a>

See the following system requirements for Lumberyard\. If you already installed Lumberyard, you can use Lumberyard Setup Assistant to see the requirements for the tools and features that you want for developing your game project\. Lumberyard Setup Assistant provides information about installing third\-party software and SDKs on your computer\. For more information, see [Using Lumberyard Setup Assistant to Set Up Your Development Environment](lumberyard-launcher-intro.md)\. 

**Topics**
+ [Operating System](#required-operating-systems-for-lumberyard)
+ [Required Hardware](#required-hardware-for-lumberyard)
+ [Developer Tools](#required-developer-tools-for-lumberyard)

## Operating System<a name="required-operating-systems-for-lumberyard"></a>

Lumberyard requires one of the following operating systems:
+ Windows 7 64\-bit
+ Windows 8\.0
+ Windows 10

## Required Hardware<a name="required-hardware-for-lumberyard"></a>

Lumberyard requires the following hardware:
+ 3GHz minimum quad\-core processor
+ 8 GB RAM minimum
+ 2 GB minimum DirectX 11 or later compatible video card
+ NVIDIA driver version 368\.81 or AMD driver version 16\.15\.2211 graphics card
+ 60 GB minimum of free disk space

Lumberyard requires the following hardware to compile builds:
+ 14 GB RAM minimum

**Note**  
Specify the `--max-cores` parameter in Waf to set the maximum number of compilation jobs\. The default value is `0`, which automatically determines the appropriate number of compilation jobs\.  
Specify the `--max-parallel-link` parameter in Waf to set the number of linker processes that simultaneously generate executable files\.  
For more information, see [Waf User Settings \(user\_settings\.options\)](waf-files-user-settings.md)\.

## Developer Tools<a name="required-developer-tools-for-lumberyard"></a>

Lumberyard requires the following developer tools:

### Visual Studio<a name="lumberyard-visual-studio-requirement"></a>

You must have one or both of the following versions of Visual Studio to compile Lumberyard Editor and tools:
+ Visual Studio 2017 version 15\.9\.2
+ Visual Studio 2015 Update 3 or later

#### Visual Studio 2017 Installation Requirements<a name="visual-studio-installation-requirements-2017"></a>

The Visual Studio 2017 default installation may not include all of the required features to run Lumberyard\. Ensure these features are selected during installation\. 

**To verify your current installation of Visual Studio 2017**

1. From Windows, click **Control Panel**, **Programs and Features**, **Microsoft Visual Studio *version\_number***\.

1. Select **Modify**\.

1. On the **Workloads** tab, do the following:
   + Select **Universal Windows Platform Development** and select the following:
     + **C\+\+ Universal Windows Platform tools**
     + **Graphics debugger and GPU profiler for DirectX**
   + Select **Game development with C\+\+** and select the following:
     + **Windows 8\.1 SDK and UCRT SDK**

1. On the **Individual components** tab, under **Compilers, build tools, and runtime**, select the following:
   + You must select at least one version of the **VC\+\+ 2017 toolset**\.

**Note**  
Beginning with Visual Studio 2017, Microsoft now releases updates on a more frequent cadence \(in some cases weekly\)\. Lumberyard is tested with the latest version of Visual Studio available during the release cycle\.

#### Visual Studio 2015 Installation Requirements<a name="visual-studio-installation-requirements-2015"></a>

The Visual Studio 2015 default installation may not include all of the required features to run Lumberyard\. Ensure these features are selected during installation\. 

**Note**  
Lumberyard does not support using only Visual C\+\+ Build Tools 2015\.

**To verify your current installation of Visual Studio 2015**

1. From Windows, click **Control Panel**, **Programs and Features**, **Microsoft Visual Studio *version\_number***\.

1. Select **Modify** and under **Programming Languages**, **Visual C\+\+**, select the following:
   + **Common Tools for Visual C\+\+ 2015**

To use both versions of Visual Studio, see [Configuring Visual Studio 2015 and 2017 for Lumberyard](lumberyard-launcher-using.md#lumberyard-launcher-visual-studio-configuration)\.

### Visual C\+\+ Redistributable Packages for Visual Studio 2012, 2013, 2015, and 2017<a name="lumberyard-visual-studio-redistributable-packages-requirement"></a>

If you do not already have Visual C\+\+ Redistributable Packages for Visual Studio installed, do one of the following:
+ After you have installed Lumberyard, run the redistributable installers from the Visual Studio \(2012, 2013, 2015, and 2017\) directories in the following directory: `lumberyard_version\dev\Tools\Redistributables\`
+ Download and run the installer directly from Microsoft:
  + [ Visual C\+\+ Redistributable Packages for Visual Studio 2012 ](https://www.microsoft.com/en-us/download/details.aspx?id=30679)
  + [Visual C\+\+ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
  + [Visual C\+\+ Redistributable Packages for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
  +  [Visual C\+\+ Redistributable Packages for Visual Studio 2017](https://www.visualstudio.com/downloads/) 