# Lumberyard 1\.10<a name="lumberyard-migrating-1-10"></a>

Use the following instructions if you are upgrading your projects to Lumberyard 1\.10\.

## Upgrading Projects<a name="lumberyard-migrating-1-10-upgrade-projects"></a>

If you created your project in Lumberyard 1\.9 or earlier, you must enable the **LmbrCentral Gem** in order to compile your project using Lumberyard 1\.10\.

If you do not follow these steps before configuring and compiling your project, you see the following error message:


****  

|  | 
| --- |
| Could not find a task generator for the name 'LmbrCentral'\. Please verify that your selected project is configured to be built\. Current Settings: Spec: '', Config: 'project\_generator', Platform 'project\_generator'  | 

For more information, see [Using Gems to Add Modular Features and Assets](gems-system-gems.md)\.

**To enable the LmbrCentral gem in the Project Configurator**

1. In the Project Configurator, select your project and click **Set as default**\.

1. Click **Enable Gems**\.

1. The Project Configurator automatically adds the **LmbrCentral Gem** and notifies you of this change\. Older `LmbrCentral` entries are also automatically removed from the `Game.xml` and `Editor.xml` configuration files\.

1. Click **Save**\.

1. Open a command line window and navigate to the `lumberyard_version\dev` directory\.

1. Enter the following command:

   ```
   lmbr_waf configure.
   ```

1. Do one of the following to build your project:
   + In Visual Studio, for **Build Configuration**, select one of the **\[Game\]** specs\. You can use **\[Game\] Profile** to start\.
   + In a command line window, enter the following command for your version of Visual Studio:

     ```
     lmbr_waf build_win_x64_vs2015_profile -p game
     ```

**To update your project using the command line**

1. Navigate to the `lumberyard_version\dev\Tools\LmbrSetup\Win` directory\.

1. Launch the `lmbr.exe` command line tool\.

1. Enter the following command to set the active project to the project that you want to update: 

   ```
   lmbr.exe projects set-active project_name
   ```

1. \(Optional\) Enter the following command to validate that the active project is set correctly: 

   ```
   lmbr.exe projects get-active
   ```

1. Enter the following command: 

   ```
   lmbr.exe projects populate-appdescriptors
   ```

1. If there is no output, the `gems.json` and configuration files are updated\.

## Updating the Editor and Game Configuration Files<a name="lumberyard-1-10-update-editor-game-configuration-files"></a>

When you upgrade your project from Lumberyard 1\.9 to Lumberyard 1\.10, you may need to remove `LmbrCentral` references from the `editor.cfg` and `game.cfg` files for your project\. `LmbrCentral` is now a gem\.

The Project Configurator automatically updates the `editor.cfg` and `game.cfg` files for your project\. However, you may receive compile errors if you do not run the Project Configurator\.

**To automatically update the configuration files**

1. Open the **Project Configurator**\. For more information, see [Creating and Switching Game Projects](configurator-projects.md)\.

1. In the **Project Configurator**, choose your project and click **Set as default**\.

1. Under your project name, choose **Enable Gems**\.

1. On the **Enable Gems** page, click **Save**\.

For reference, the previous XML appeared as follows:

```
<Class name="DynamicModuleDescriptor" field="element" type="{D2932FA3-9942-4FD2-A703-2E750F57C003}">
<Class name="AZStd::string" field="dynamicLibraryPath" value="LmbrCentral" type="{EF8FF807-DDEE-4EB0-B678-4CA3A2C490A4}"/>
</Class>
```

The new XML appears as follows:

```
<Class name="DynamicModuleDescriptor" field="element" type="{D2932FA3-9942-4FD2-A703-2E750F57C003}" specializationTypeId="{D2932FA3-9942-4FD2-A703-2E750F57C003}">
<Class name="AZStd::string" field="dynamicLibraryPath" type="{EF8FF807-DDEE-4EB0-B678-4CA3A2C490A4}" value="Gem.LmbrCentral.ff06785f7145416b9d46fde39098cb0c.v0.1.0" specializationTypeId="{189CC2ED-FDDE-5680-91D4-9F630A79187F}"/>
</Class>
```

## Upgrading Your Starter Game Project<a name="lumberyard-migrating-1-10-starter-game"></a>

Starter Game has been updated for Lumberyard 1\.10 compatibility\.

If you have been making your own changes to Lumberyard 1\.9 Starter Game, you must upgrade your existing Starter Game project to avoid losing your work when upgrading to Lumberyard 1\.10\.
+ Material lifetime has been updated in order to address stability issues\. As a result, any code or classes that store an IMaterial\* in C\+\+ are no longer valid\. You must convert any code that acquires and stores an IMaterial\* to `_smart_ptr<IMaterial>`\. 
+ Enable the [LmbrCentral Gem](#lumberyard-migrating-1-10-upgrade-projects) to compile your project in 1\.10\.
+ [Build your project](building-your-lumberyard-game-project.md)\.

## Converting AZ::IO::Print to PrintV<a name="lumberyard-migrating-1-10-convert-az-print-function"></a>

In Lumberyard 1\.9 and earlier, the `AZ::IO::Print` function had two implementations:
+ `int64_t Print(HandleType fileHandle, const char* format, ...);`
+ `int64_t Print(HandleType fileHandle, const char* format, va_list arglist);`

In Lumberyard 1\.10, the second implementation is now `PrintV` instead of `Print`: `int64_t PrintV(HandleType fileHandle, const char* format, va_list arglist);`

If you use the second implementation, you must update the function name to use `PrintV`:
+ Lumberyard 1\.9 and earlier: `AZ::IO::Print(fileHandle, format, arglist);`
+ Lumberyard 1\.0: `AZ::IO::PrintV(fileHandle, format, arglist);`