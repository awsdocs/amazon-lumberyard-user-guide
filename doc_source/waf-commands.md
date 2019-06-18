# Waf Commands and Options<a name="waf-commands"></a>

**Contents**
+ [Waf Configuration](#waf-configuration)
+ [Build Configuration](#build-configuration)
+ [Multiplayer Configuration](#waf-multiplayer-configuration)

Before building a project using Waf, you must run configure from the command line\. The configure command recursively processes all of the wscript configuration files starting from the root directory and generates a Visual Studio solution file for the entire project\. You can set an option to generate a solution file during the configure command\.

**Note**  
The Waf script automatically runs Lumberyard Setup Assistant to ensure the correct third\-party libraries are available and the proper links are created to compile the game code, engine and asset pipeline, and editor and tools\.

## Waf Configuration<a name="waf-configuration"></a>

To run the Waf executable, run the following command at the `lumberyard_version\dev\` directory of your project:

lmbr\_waf configure

This command iterates through all the Waf project configuration files and sets up the project\-specific settings in the Waf cache, which is used in subsequent build commands\. It also uses the host environment to determine which platforms are available to build\.

**Example**  
The following example shows the output of the lmbr\_waf configure command:  

```
[WAF] Executing 'configure'
Running SetupAssistant.exe...
--- Lumberyard Setup Assistant ---
SDK location: d:/lumberyard_engine/dev
Third party location: d:/lumberyard_engine/dev/3rdParty
Capabilities Available, [x] enabled  - [ ] disabled:
[ ] rungame - Run your game project
[ ] runeditor - Run the Lumberyard Editor and tools
[X] compilegame - Compile the game code
[X] compileengine - Compile the engine and asset pipeline
[X] compilesandbox - Compile the Lumberyard Editor and tools
[ ] compileandroid - Compile for Android devices
[ ] compileios - Compile for iOS devices
Successfully executed
[INFO] Configure "win_x64_vs2017 - [debug, profile, performance, release, debug_dedicated, profile_dedicated, performance_dedicated, release_dedicated]"
[INFO] Configure "win_x64_vs2015 - [debug, profile, performance, release, debug_dedicated, profile_dedicated, performance_dedicated, release_dedicated]"


[INFO] Configure "android_armv7_gcc - [debug, profile, performance, release, debug_dedicated, profile_dedicated, performance_dedicated, release_dedicated]"
[WARN] Removing the following Android target platforms due to "Compile For Android" not checked in Setup Assistant.
        -> android_armv7_gcc, android_armv7_clang
[WAF] 'configure' finished successfully (10.335s)
[WAF] Executing 'generate_uber_files' in 'd:\ws\lyengine\dev\BinTemp'
[WAF] 'generate_uber_files' finished successfully (2.177s)
[WAF] Executing 'msvs' in 'd:\ws\lyengine\dev\BinTemp'
```

The configure command uses the settings defined in the `user_settings.options` file that is located in the `_WAF_` subfolder\. You can edit this file in a text editor or use the built\-in settings editor: lmbr\_waf show\_option\_dialog

If you set the option to generate a Visual Studio solution to **true**, a solution file is created in the directory specified in the `user_settings.option` file\. If you do not modify the `user_settings.option` file, the Visual Studio solution is in `lumberyard_version/Solutions/LumberyardSDK.sln` by default\.

## Build Configuration<a name="build-configuration"></a>

After configuring Waf, you can run the build command\.

The following example shows the syntax: 

```
lmbr_waf build_platform_configuration -p spec
```

The following commands and options are available:
+ configure – Must be run before any clean or build command\. Loads all modules, configs, and project specs; validates and sets up the working cached build Python file\.
+ build\_\* – Builds the specified project spec for the specified platform and configuration\.
+ clean\_\* – Cleans out intermediate and target files that were generated for the particular platform and configuration\.

The following example shows how to build release for Windows x64 with Visual Studio 2015: 

```
lmbr_waf build_win_x64_vs2015_release -p all
```

**Note**  
Combining the clean\_\* and build\_\* commands is the equivalent of performing a rebuild\.


**Configure command options**  

| Command | Command Option | Description | 
| --- | --- | --- | 
| build\_\*, clean\_\* | \-p spec name \-\-project\-spec=spec name  | The spec name to use to build or clean a project\. | 
|  | \-\-targets=target1,target2,\.\.\. | Optional flag to filter on which targets to build\. The targets must be included in the project spec above in order for this to work\. | 
| build\_\*, clean\_\*, configure | \-\-profile\-execution=\(True\|False\) | The option to run the build process through the Python execution profiler\. As this will produce a large output to the console, we recommend that you redirect the output of this command to a log file\. | 
| build\_\* | \-\-execsolution=VS\_solution\_path | This internally\-generated command line is a Visual Studio solution that provides a way to build Waf commands invoked from the VS IDE to apply additional overrides that can be defined in the \.vcxproj files themselves\. | 
| build\_\* | \-\-file\-filter=source\_files | An option to pass in a comma\-separated list of absolute paths to source files to filter the build on\. This option is useful to build specific files\. | 
| build\_\* | \-\-show\-includes=\(True\|False\) | Option to show the \#include tree that a file uses during compilation\. This option is only valid when \-\-file\-filter is specified\. | 
| build\_\* | \-\-show\-preprocessed\-file=\(True\|False\) | Option to generate a preprocessor output for a source file \(but not actually build the file\)\. The generated file is saved in the variant folder under \\bintemp based on the location of the source file\. This option is only valid when \-\-file\-filter is specified\. | 
| build\_\* | \-\-show\-disassembly=\(True\|False\) | Option to generate an Assembler output for a source file \(but not actually build the file\)\. The generated file is saved in the variant folder under \\bintemp based on the location of the source file\. This option is only valid when \-\-file\-filter is specified\. | 
| configure | \-\-update\-settings=\(True\|False\) | Option to update the user\_settings\.options file with any values that are modified from the command line\. For instance, if you want to modify the value of use\_uber\_files in user\_settings\.options, set \-\-use\-uber\-files=True in the command line for configure and add \-\-update\-settings=True to apply the changes to user\_settings\.options\. | 

You can set the command options at build time\. These options override the values set in the `user_settings.option` file\. For more information, see [Project Configurator](waf-files-user-settings.md)\.

Only modules that support each project configuration are built from the project spec\. If a module is defined in the spec that only can be built in debug or profile, building in performance mode excludes that project from compilation\.<a name="build-parameters"></a>


**Project configurations parameters**  

| Configuration | Asserts | Profiling | Optimization | Logging | Description | 
| --- | --- | --- | --- | --- | --- | 
| debug | Yes | All | Minimum | Yes | Slowest – Focuses on debugging with asserts enabled, all profiling features enabled, and logging enabled\. | 
| profile | No | All | Medium | Yes | Fast – Strikes a balance between debugging and performance with all profiling features and logging enabled\. | 
| performance | No | Few | Maximum | No | Very fast – Performance similar to release but has some profiling features enabled; difficult to debug; no logging\. | 
| release | No | None | Maximum | No | Fastest – Highest performance; most difficult to debug; no profiling features; no logging\. | 


**Build command project spec options**  

| Spec | Platform | Configuration | Description | 
| --- | --- | --- | --- | 
| all | win\_x64\_vs2017, win\_x64\_vs2015, darwin\_x64 | Debug, profile, performance, release | Configuration to build the engine, editor, plugins, and tools | 
| game\_and\_engine | win\_x64\_vs2017, win\_x64\_vs2015, darwin\_x64, linux\_x64 | Debug, profile, performance, release | Configuration to build the engine and game project | 
| dcc\_plugins | win\_x64\_vs2017, win\_x64\_vs2015 | Debug, profile | Configuration to build tools for the asset pipeline | 
| resource\_compiler | win\_x64\_vs2017, win\_x64\_vs2015 | Debug, profile | Configuration to build the Resource Compiler only | 


**Build configuration options**  

| Option | Description | 
| --- | --- | 
| \-\-progress | Shows the build progress and updates in real time\. | 
| \-\-project\-spec | Specifies the project spec to use when cleaning or building the project\. | 
| \-\-show\-includes | Shows the includes for each compiled file\. | 
| \-\-target | Specifies the target to build and its dependencies\. The target must exist in the specified project spec; otherwise, all targets in the project spec are built\. | 

## Multiplayer Configuration<a name="waf-multiplayer-configuration"></a>

Before you can build multiplayer information, you must build the dedicated server\. This creates a directory called `Bin64.Dedicated` that includes the binaries directory and configuration files for the dedicated server\.

To build the dedicated server, run the following build command for your version of Visual Studio:

```
lmbr_waf build_win_x64_vs2015_profile_dedicated -p dedicated_server
```