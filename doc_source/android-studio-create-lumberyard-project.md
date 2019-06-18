# Creating a Lumberyard Project for Android Studio<a name="android-studio-create-lumberyard-project"></a>

You can use a PC or Mac to create your Lumberyard Android Studio project\.

**To create an Android Studio project**

1. In a command line window, navigate to the root of the directory where you installed Lumberyard \(`lumberyard_version\dev` on PC or `~/lumberyard_version/dev` on Mac\)\.

1. Run the following command: `lmbr_waf configure`
**Note**  
The `configure` command automatically generates the Android Studio project\. To disable this functionality and manually generate an Android Studio project, edit the `user_settings.options` file \(located in the `lumberyard_version\dev\_WAF_` directory\) to change the **generate\_android\_studio\_projects\_automatically** option from **True** to **False**\. Then run `lmbr_waf android_studio` or `lmbr_waf configure android_studio` \(if base projects were not created from a previous `configure` command\)\.

1. Verify the Android Studio project was created successfully: 

   ```
   [WAF] Executing 'android_studio' in 'C:\Lumberyard\dev\BinTemp'
   [INFO] Created at C:\Lumberyard\dev\Solutions\LumberyardAndroidSDK
   [WAF] 'android_studio' finished successfully (1.261s)
   ```