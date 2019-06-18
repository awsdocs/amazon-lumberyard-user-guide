# Lumberyard 1\.9<a name="lumberyard-migrating-1-9"></a>

Lumberyard 1\.9 includes an upgrade script that helps you to change the version of the AWS Native SDK that you use\.

## AWS Native SDK Upgrade Script<a name="lumberyard-migrating-1-9-sdk-upgrade-script"></a>

To help automate the process of downloading and installing `.zip` files from the AWS SDK for C\+\+ [prebuild site](http://sdk.amazonaws.com/cpp/builds/index.html), you can run an upgrade script\. The script downloads files from the prebuild site and adds them to your `3rdParty` directory\. By default, the script installs prebuilds of all platforms and services that are included with Lumberyard\.

You can use the script to do the following:
+ Change the version of the `AWSNativeSDK` that Lumberyard uses\.
+ Add or remove the list of services available within Lumberyard\.

When you change the version or add or remove services, you must also modify the corresponding configuration files `SetupAssistantConfig.json`, `aws_native_sdk_shared.json`, and `aws_native_sdk_static.json` files\.

### Running the Upgrade Script<a name="lumberyard-migrating-1-9-running-the-upgrade-script"></a>

The `Upgrade.py` script is located in the `\dev\Tools\AWSNativeSDK\Upgrader` directory\. The Python executable file must be in your Windows environment path\.

To run the script, enter the following syntax:

```
python upgrade.py <version> <optional destination>
```

The following example command specifies SDK version 1\.0\.74\.

```
python upgrade.py 1.0.74 F:\3rdParty\AWS\AWSNativeSDK\1.0.74
```

#### Parameters<a name="lumberyard-migrating-1-9-upgrade-script-parameters"></a>

*<version>* – Specifies the SDK version number\. To change the version that Lumberyard uses, you must also change the corresponding version numbers in the `dev\SetupAssistantConfig.json` file\. For more information, see [Changing Version Numbers](#lumberyard-migrating-1-9-upgrade-script-changing-version-numbers)\.

*<optional destination>* – Specifies the AWS Native SDK installation location\. The default location is the Lumberyard `3rdParty` directory\. If you use a different directory, specify the directory path in this parameter\.

### Changing Version Numbers<a name="lumberyard-migrating-1-9-upgrade-script-changing-version-numbers"></a>

To change SDK versions, you must change the version numbers in the `dev\SetupAssistantConfig.json` file\. Modify the locations in the file as indicated in the following example\.

```
{
    "identifier": "AWSNativeSDK",
    "name": "AWSNativeSDKName",
    "version": "1.0.74",                          <-----   Change version number
    "source": "AWS/AWSNativeSDK/1.0.74",          <-----   Change version number
    "optional": 0,
    "description": "AWSNativeSDKDescriptionSummary",
    "detailedInstructions": "AWSNativeSDKDetailedInstructions",
    "roles": [ "compilegame", "compileengine", "compileeditor", "compileios", "compileandroid", "setuplinux" ],
    "symlinks": [
        {
            "source": "AWS/AWSNativeSDK/1.0.74",   <-----   Change version number here and in
                                                            similar following occurrences.
```

### Customizing Platforms and Services<a name="lumberyard-migrating-1-9-upgrade-script-customizing-platforms-and-services"></a>

To customize platforms and services, modify the code in the `Upgrade.py` script\.

#### Customizing Platforms<a name="lumberyard-migrating-1-9-upgrade-script-customizing-platforms"></a>

To customize the list of platforms that you use, modify the `get_platform_list():` call\. The following code shows the default platform list\.

```
def get_platform_list():
    platform_list = []

    platform_list.append(get_windows_vs2017())
    platform_list.append(get_windows_vs2015())
    platform_list.append(get_darwin())
    platform_list.append(get_ios())
    
    platform_list.append(get_appletv())
    platform_list.append(get_android())
    platform_list.append(get_linux())
```

#### Customizing Services<a name="lumberyard-migrating-1-9-upgrade-script-customizing-services"></a>

To customize services for all platforms or individual platforms, modify the script as in the following example for Microsoft Visual Studio 2015 on Windows\.

```
def get_windows_library_list():
    return_list = get_default_library_list()

    ## Libraries by customer request
    return_list.append('access-management')
    return_list.append('transfer')

    return return_list

def get_windows_vs2015():
    vs2015 = {}
    vs2015['platform'] = 'windows'
    vs2015['zipfile'] = 'aws-sdk-cpp_x86_64_visual_cpp-14x.zip'
    vs2015['libraries'] = get_windows_library_list()
    vs2015['libextensions'] = ['.dll', '.lib']

    return vs2015
```

To add a service to Windows, add the service to `get_windows_library_list()`\. The following example adds the `polly` service to Windows\.

```
return_list.append('polly') 
```

##### Making a Service Accessible to Wscript<a name="lumberyard-migrating-1-9-upgrade-script-wscript"></a>

To make a service accessible within your `.wscript` files, add the service name to the `dev\_WAF_\3rdParty\aws_native_sdk_shared.json` and `dev\_WAF_\3rdParty\aws_native_sdk_static.json` files\.