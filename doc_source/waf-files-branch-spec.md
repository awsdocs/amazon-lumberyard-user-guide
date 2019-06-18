# Waf Branch Spec \(waf\_branch\_spec\.py\)<a name="waf-files-branch-spec"></a>

The `waf_branch_spec.py` is the topmost configuration level of the Waf build system\. It specifies which operating systems and configurations are available for all projects and specs\.

The following is an example `waf_branch_spec.py` file:

```
######################
## Build Layout
BINTEMP_FOLDER = 'BinTemp'
 
######################
## Build Configuration
COMPANY_NAME = 'My Company'
COPYRIGHT = '(c) My Company'
 
######################
## Supported branch platforms/configurations
## This is a map of host -> target platforms
PLATFORMS = {
    'darwin' :  [ 'darwin_x64', 'android_armv7_gcc', 'ios' ],
    'win32' :   [ 'win_x64', 'win_x64_vs2012', 'win_x64_vs2010', 'android_armv7_gcc' ],
    'linux' :   [ 'linux_x64_gcc', 'linux_x64_clang' ]
    }
 
## And a list of build configurations to generate for each supported platform
CONFIGURATIONS = [ 'debug',           'profile',           'performance',           'release',
                   'debug_dedicated', 'profile_dedicated', 'performance_dedicated', 'release_dedicated' ]
 
## what conditions do you want a monolithic build ?  Uses the same matching rules as other settings
## so it can be platform_configuration, or configuration, or just platform for the keys, and the Value is assumed
## false by default.
## monolithic builds produce just a statically linked executable with no dlls.
 
MONOLITHIC_BUILDS = {
        'release' : True,
        'release_dedicated' : True,
        'performance_dedicated' : True,
        'performance' : True,
        'ios' : True
        }
```

The waf\_branch\_spec\.py file manages the following global values:


**Global values**  

| Value | Description | 
| --- | --- | 
| ADDITIONAL\_COPYRIGHT\_TABLE | Optional additional table of copyrights\. To add a company specific copyright, add a name value pair to define the desired copyright statement for generated binaries and add the 'copyright\_org' in your wscript definition  | 
| BINTEMP\_FOLDER | Subfolder under the base of the project where Waf stores all intermediate and temporary files | 
| COMPANY\_NAME | Company name to embed in the built executables | 
| CONFIGURATIONS | List of possible build configurations | 
| COPYRIGHT | Copyright header to embed in the built executables | 
| MONOLITHIC\_BUILDS | Build configurations mapped to monolithic flag values | 
| PLATFORMS | Supported host platforms mapped to corresponding build platforms | 