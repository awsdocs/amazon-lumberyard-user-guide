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
For more information, see [Waf User Settings \(user\_settings\.options\)](waf-user-options-and-settings.md#waf-files-user-settings)\.

## Developer Tools<a name="required-developer-tools-for-lumberyard"></a>

Lumberyard requires the following developer tools:

### Visual Studio<a name="lumberyard-visual-studio-requirement"></a>

You must have at least one of the following versions of Visual Studio to compile the game code, compile the engine and asset pipeline, or compile the Lumberyard Editor and tools:
+ Visual Studio 2019 version 16\.2\.4 or above
+ Visual Studio 2017 version 15\.9\.14 or above

**Note**  
The definitive source for the minimum version of Visual Studio for any particular release of Lumberyard is set in the file `dev\_WAF_\settings\platforms\platform.win_x64_vs2019.json`\. Look for the **vswhere\-args** settings\. The minimum version is the first value in the **default\_value** range\.

#### Visual Studio 2017 and 2019 Installation Requirements<a name="visual-studio-installation-requirements"></a>

The Visual Studio default installation might not include all of the required features to run Lumberyard\. Ensure these features are selected during installation\. 

**To verify your current installation of Visual Studio 2017 or Visual Studio 2019**

1. From Windows, either launch the **Visual Studio Installer** or click **Control Panel**, **Programs and Features**, **Microsoft Visual Studio *version\_number***\.

1. Select **Modify**\.

1. On the **Workloads** tab, do the following:
   + Select **Game development with C\+\+** and select the following:
     + You must select at least one version of the **Windows 10 SDK**\.

1. On the **Individual components** tab, under **Compilers, build tools, and runtimes**, do the following:
   + Select a **VC\+\+ toolset** that corresponds to the version of Visual Studio that you have installed:
     + You must select at least one version of the **VC\+\+ 2017 toolset** to build using Visual Studio 2017\.
     + You must select at least one version of the **MSVC v142 \- VS 2019 C\+\+ x64/x86 build tools** to build using Visual Studio 2019\.
   + \(Optional\) Select **MSVC v141 \- VS 2017 C\+\+ x64/x86 build tools** to allow Visual Studio 2019 to build using the Visual Studio 2017 toolset\.

**Note**  
Incredibuild users: Installing, reinstalling, or upgrading Visual Studio may cause the Incredibuild Agent to lose its settings or require an update\. After modifying Visual Studio, be sure to confirm your Incredibuild Agent is active\. For instructions on configuring the agent properly, see [Compiling with IncrediBuild](waf-extensions.md#waf-extensions-incredibuild)\.

**Note**  
Beginning with Visual Studio 2017, Microsoft now releases updates on a more frequent cadence \(in some cases weekly\)\. Lumberyard is tested with the latest version of Visual Studio available during the release cycle\.

### Visual C\+\+ Redistributable Packages for Visual Studio 2012, 2015, 2017, and 2019<a name="lumberyard-visual-studio-redistributable-packages-requirement"></a>

If you do not already have Visual C\+\+ Redistributable Packages for Visual Studio installed, do one of the following:
+ After you have installed Lumberyard, run the redistributable installers from the Visual Studio directories in the following directory: `lumberyard_version\dev\Tools\Redistributables\`
+ Or, download and run the installer directly from Microsoft:
  +  [Visual C\+\+ Redistributable Packages for Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30679)
  +  [Visual C\+\+ Redistributable Packages for Visual Studio 2015–2019](https://visualstudio.microsoft.com/downloads/#other-family) 

**Note**  
The Visual Studio redistributable for Visual Studio versions 2015 through 2019 are now included in one installer\. On the Visual Studio download web page, it may be labelled **Microsoft Visual C\+\+ Redistributable for Visual Studio 2019**\.