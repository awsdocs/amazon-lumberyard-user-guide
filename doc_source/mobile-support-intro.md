# Creating Android and iOS Games<a name="mobile-support-intro"></a>

You can use Lumberyard to build your games for Android devices and iOS devices that use the A8 GPUs\. Lumberyard includes two Android\-supported sample projects and four iOS\-supported sample projects that you can use to learn how to build assets, build shaders using the remote shader compiler, and build the Lumberyard runtime \(Android\) or iOS applications using the Lumberyard build tools\.

Lumberyard supports the following minimum specifications for Android and iOS:


****  

|  | Android | iOS | 
| --- | --- | --- | 
| CPU | ARM quad\-core or newer\(for example, ARM Krait 400, Cortex\-A53\) | ARM v8 or newer | 
| GPU | Adreno 330, Mali\-T760 or newerSupports OpenGL 3\.0 | PowerVR G6430 \(quad\-core\) or newerSupports Metal | 
| OS | 5\.1 or newer | iOS 7\.0 or newer | 
| Example devices | Samsung Galaxy Note 4LG Nexus 5Kindle Fire HDX | iPhone 5s and newer | 

**Topics**
+ [Android Support](android-intro.md)
+ [iOS Support](ios-intro.md)
+ [Design Considerations for Creating Mobile Games Using Lumberyard](ios-android-design-considerations.md)
+ [Lumberyard Performance Tuning Guidelines for Mobile Devices](ios-android-performance-guidelines.md)
+ [Modifying Project Settings for Mobile Device Games](mobile-project-settings-tool.md)
+ [Updating Graphics Settings for Android and iOS](ios-android-updating-graphics-settings.md)
+ [Adding IP Addresses to Allow Access to the Asset Processor and Remote Console](ios-android-adding-ip-addresses.md)
+ [Running the Shader Compiler on Amazon EC2](ios-android-running-shader-compiler-amazon-EC2.md)
+ [Using AppDetective to Test Your Game Build on the AWS Device Farm](ios-android-appdetective.md)