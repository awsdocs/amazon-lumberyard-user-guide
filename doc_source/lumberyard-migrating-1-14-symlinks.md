# Symlinks Removed for Third\-Party Libraries<a name="lumberyard-migrating-1-14-symlinks"></a>

Lumberyard 1\.14 does not generate or use symlinks as it did in previous versions\. Instead, WAF keeps track internally of the relationship between each third\-party library and its absolute path\. 

Previously, the bootstrap process generated symbolic links \(directory junctions in Windows\) based on the settings file that Lumberyard Setup Assistant configured\. Lumberyard executed WAF build commands only after this bootstrap process was complete\. 

**Note**  
The bootstrap process is still required even without symlink generation\.

The removal of symlinks provides the following advantages:
+ Provides an OS\-independent management way of handling external directories by managing third\-party locations internally with WAF\.
+ Removes necessity of checking for stale links\.
+ Resolves issues with Perforce \(P4\) recursions\.
+ Makes packaging up the engine tree easier because you don't need to exclude the SDK directories\.
+ Solves issues with some operating systems where a clean directory may recurse into the SDKs directories and remove their contents\.

The removal of symlinks has the following limitations:
+ Source of third\-party directories are not readily apparent when observing the file structure\.
+ Source code cannot easily refer to SDK locations at runtime\.

The following sections describe the now deprecated symlink approach of referring to third\-party files and the new approach without symlinks\.

**Topics**
+ [Deprecated Symlink System](#lumberyard-migrating-1-14-symlinks-old)
+ [New Approach Without Symlinks](#lumberyard-migrating-1-14-symlinks-new)

## Deprecated Symlink System<a name="lumberyard-migrating-1-14-symlinks-old"></a>

Prior to Lumberyard 1\.14, the symlink solution system aggregated external directories into the following SDKs directories:
+ `lumberyard_version\dev\code\SDKs`
+ `lumberyard_version\dev\code\Sandbox\SDKs`
+ `lumberyard_version\dev\code\Tools\SDKs`

Lumberyard Setup Assistant created these parent directories during the bootstrap process and generated the symlinks after Lumberyard Setup Assistant requirements were met\.

### Direct Path Reference<a name="lumberyard-migrating-1-14-symlinks-old-direct"></a>

In WAF files \(like the wscripts\), references to third\-party directories had to resolve one of the SDKs directories listed in the previous section\. The build context included a method called `Path` that resolved to the root of the engine folder\. 

**Example**  
The following `IOSLauncher` wscript file demonstrates this\. The library paths are based on the symlinks generated for LibTomCrypt, LibTomMath, and FreeType2\.  

```
bld.CryLauncher(
    #==============================
    # Settings
    #==============================
    target           = 'IOSLauncher',
    file_list        = 'ioslauncher.waf_files',
    platforms        = ['ios'],
    configurations   = ['debug', 'profile', 'performance', 'release'],
    ios_launcher     = True,
    use              = ['AzGameFramework'],
 
    #==============================
    # Common
    #==============================
    includes        = [ bld.Path('Code/CryEngine/CrySystem'),
                        bld.Path('Code/Launcher') ],
 
    lib     = [ 'tommath',
                'tomcrypt',
                'freetype' ],
 
    libpath = [ bld.Path('Code/SDKs/LibTomCrypt/lib/ios'),
                bld.Path('Code/SDKs/LibTomMath/lib/ios'),
                bld.Path('Code/SDKs/FreeType2/ios/lib') ],
 
    cxxflags        = [ '-x', 'objective-c++' ],
    )
```

In the new approach that no longer uses symlinks, the `libpath` section would look like the following example\. For more information, see [Direct Path Alias](#lumberyard-migrating-1-14-symlinks-new-direct)\.

**Example**  

```
...

libpath = [ bld.Path('@3P:libtomcrypt@/lib/ios'),
            bld.Path('@3P:libtommath@/lib/ios'),
            bld.Path('@3P:freetype2@/ios/lib') ],
...
```

### Third\-Party Library References<a name="lumberyard-migrating-1-14-symlinks-old-thirdparty"></a>

Lumberyard extracted the third\-party libraries with the third\-party library mechanism\. The definition files for each third\-party reference library is in `lumberyard_version\dev\_WAF_\3rdParty` directory\. If the third\-party library is consumed through the \(proper\) `use` or `uselib` mechanism, the third\-party library's definition references the source directly based on the symlink location\. 

**Example**  
The following demonstrates the definition for boost \(`lumberyard_version\dev\_WAF_\3rdParty\boost.json`\)\. The source root `"source"` refers to the symlink generated for boost at `Code\SDKs\boost`\.  

```
{
   "name": "boost",
   "source": "@ROOT@/Code/SDKs/boost",
   "description": "Boost header only library",
   "header_only": "True",
   "includes": [
      "."
   ],
   "defines": [],
   "lib_required": "False"
}
```

### Direct Source File References<a name="lumberyard-migrating-1-14-symlinks-old-directref"></a>

In some cases, the source file of a third\-party library was added directly\. WAF used `*.waf_files` to define which files \(relative to the `waf_files`\) to add for the module\. With symlinks, relative paths backtracked to the SDK's directories to refer to the source file\.

**Example**  
The following example shows the `waf_files` definition for `ResourceCompilerABC`\. The `mikktspace.cpp` file in the `mikkelsen` library is referenced\.  

```
...
"MeshCompiler (Cry3DEngine)":
[
    "../../../SDKs/TangentBasisComputation/mikkelsen/mikktspace.cpp"
],
...
```

## New Approach Without Symlinks<a name="lumberyard-migrating-1-14-symlinks-new"></a>

The new approach does not create the three SDKs directories in the `Code` subdirectory\. Instead, third\-party file locations are managed under a working file, `Bintemp\3rdParty.json`\. WAF generates the `3rdParty.json` file during configuration \(when Lumberyard Setup Assistant previously generated the symlinks or junctions\)\. 

WAF generates the `3rdParty.json` configuration file, which maps third\-party identifiers in `SetupAssistantConfig.json` to the physical file locations\. To generate this file, WAF takes into account the location of the third\-party directory and the options selected in Lumberyard Setup Assistant \(such as compile game and engine, compile editor, android, and so on\)\.

The `SetupAssistantConfig.json` file lists all of the SDK identifiers under the SDKs root in each SDK's `identifier` attribute\. For example, the boost library is identified by the `boost` identifier\.

### Direct Path Alias<a name="lumberyard-migrating-1-14-symlinks-new-direct"></a>

A special alias refers to the third\-party directory\. This alias is `@3P:sdk_identifier@`, where *`sdk_identifier`* is an SDK identifer defined in the `SetupAssistantConfig.json` file\.

**Note**  
This identifier should not to be confused with the third\-party `uselib` identifier\. The third\-party `uselib` configuration files are one level above this system and uses the special alias to locate the base source directory\.

### Third\-Party Library References<a name="lumberyard-migrating-1-14-symlinks-new-thirdparty"></a>

The third\-party library reference system uses the `@3P:sdk_identifier@` alias as well\.

**Example**  
In the following example `lumberyard_version\dev\_WAF_\3rdParty\boost.json` file, the actual location for the boost uselib reference is defined\. `@3P:boost@` resolves to the source location of the boost SDK\.  

```
{
   "name": "boost",
   "source": "@3P:boost@",
   "description": "Boost header only library",
   "header_only": "True",
   "includes": [
      "."
   ],
   "defines": [],
   "lib_required": "False"
}
```

### Direct Source File References<a name="lumberyard-migrating-1-14-symlinks-new-direct-source"></a>

For direct source reference, the same `@3P:sdk_identifier@` alias is applied\. Instead of using a back reference to the SDKs directory in the `waf_files` content file, the alias is used instead\.

```
"MeshCompiler (Cry3DEngine)":
[
    "@3P:mikkelsen@/mikkelsen/mikktspace.cpp",
    "@3P:mikkelsen@/mikkelsen/mikktspace.h"
],
```