# Waf Extensions<a name="waf-extensions"></a>

## Compiling with IncrediBuild<a name="waf-extensions-incredibuild"></a>

Waf supports IncrediBuild 8\.0\.1 or later, and allows for distributed network builds for compiling larger projects\.

You must have the appropriate package for your operating system:
+ **Windows** or **Android** – IncrediBuild for Make and Build or Accelerated Dev Tools

To verify which package is configured for your machine, run the following command \(located in `C:\Program Files (x86)\Xoreax\IncrediBuild`\): `xgConsole.exe /QUERYLICENSE`

The following is output:

```
> xgConsole.exe /QUERYLICENSE
  
License details:
----------------
Registered to: My Game Company
Up to XX Agents allowed
Maintenance expires on XX/XX/XXXX
  
Packages installed:
-------------------
  - IncrediBuild for Make && Build Tools
```


****  

| To do this | Run this at a command line | 
| --- | --- | 
| Enable or disable IncrediBuild builds | use\_incredibuild Instructs Waf to use incredibuild to distribute and parallelize the build, if possible\. You need to specify the type of incredibuild package based on the platform\.  | 
| Adjust the maximum number of parallel tasks | incredibuild\_max\_cores | 
| Determine which IncrediBuild package is configured for your machine | xgConsole\.exe /QUERYLICENSE | 

Waf requires certain packages and the Windows registry key settings below to run IncrediBuild\. Run `lmbr_waf.bat` in **Administrator** mode to edit the registry\.

Modify the settings in the Windows registry under the following key:

`HKEY_LOCAL_MACHINE\\Software\\Wow6432Node\\Xoreax\\Incredibuild\\Builder`


**Registry Settings**  

| Name | Value | Description | 
| --- | --- | --- | 
| MaxConcurrentPDBs | 0 | Controls how many files can be processed in parallel\. This optimization is also useful for MSBuild\. | 

**To enable IncrediBuild**

1. Open the `user_settings.options` file located in `/_WAF_`\.

1. In the `user_settings.options` file, under **\[Incredibuild Options\]**, do the following:
   + Set the **use\_incredibuild** flag to **True**\.

1. Save your changes\.

## Compiling with QT<a name="waf-extensions-qt"></a>

Waf supports compiling QT5 `.moc` Meta\-Object\-Compiler files\. To enable or disable compiling of particular files, add the `qt5` feature to your Waf Module \(wscript\) file and then add the list of files to be compiled\.

The following example shows a Waf Module \(wscript\) file:

```
# wscript relative path
QT_TO_MOC_FILES = [
    'MyQTFile.h',
    'MyOtherQTFile.h',
    ...
    ]
 
def build(bld):   
    bld.CryPlugin(
        target      = 'MyQTPlugin',
        vs_filter   = 'Plugins',
        file_list   = 'file_list.waf_files', 
       
        features        = ['qt5'], # add the QT5 moc feature to this Waf module
       
    )
```

## Compiling with Visual Studio<a name="waf-extensions-vs"></a>

Waf has limited support for the Visual Studio 2015 IDE\. Once you run the `configure` command to generate a Visual Studio solution, you can invoke Waf through the IDE and open the solution file in Visual Studio 2015\.

Waf creates a Visual Studio solution file along with the projects specified in the selected project specs\. If more than one spec file includes the same project, only one project file is created to prevent duplicates\. Waf uses the project specs to determine the projects, project filters, and possible build configurations\. Waf uses the wscript files to identify individual project definitions\.

**To select the active solution configuration**

1. Open the solution file in Visual Studio 2015\.

1. Select **Build**, **Configuration Manager**\.

1. In the Configuration Manager dialog box, select **\[All\] Debug** from the **Active solution configuration** drop\-down list\. This option builds all x64 modules in debug mode\.

1. Click **Close**\.

Once the active solution configuration is set, you can build the solution\.

**To build the solution in Visual Studio 2015**

1. Select **Build**, **Build Solution**\. This builds all modules defined in the all project spec\.

1. Once the build is successful, you can choose different solution configurations based on your active projects\. For example, if you are working on the game \(`game_and_engine` spec\), you wouldn't need to build everything\. Or if you want to build a profile configuration of the build, you can use **\[All\] Profile**\.