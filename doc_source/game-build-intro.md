# Creating Game Builds<a name="game-build-intro"></a>

You can create a variety of game builds, including a release build\. See the following definitions for the different build mode types:

**Profile mode builds for game developers, designers, and artists**
+ Provides an optimized build meant for game development\.
+ Contains performance instrumentation and debugging output\.
+ Compiles shaders at run time, which may require the remote shader compiler\.
+ Communicates with Asset Processor and compiles as needed\.
+ Has logging, crash reporting, metrics, and other troubleshooting features\.

**Debug mode builds for programmers**
+ Provides a non\-optimized version of the game engine that provides the same features as the profile version\.
+ Has additional memory checks and tests\.
+ Provides step\-by\-step code that programmers can use to debug the execution\.

**Release mode builds for customer previews, demos, and launches**
+ Loads assets and data only from `.pak` files\.
+ Loads shaders from `.pak` files for better performance but may compile shaders for DirectX at run time if a shader is not found in the `.pak` files\.
+ Can't use virtual file system \(VFS\) or remote asset access\.
+ Doesn't communicate with Asset Processor because Asset Processor doesn't ship with the game\.
+ Removes most logging, instrumentation, profiling, and other measurement metrics\.
+ Removes all game developer and programmer features such as console usage, cheat commands, command line parsing, and batch mode processing\.
+ Combines everything into a single executable file instead of DLLs\.

To learn the general steps for creating a release build in Lumberyard, see [Simple Asset Bundling and Release Tutorial](asset-bundler-tutorial-simple.md)\. For more information about creating release builds for Android and iOS, see [Creating Android and iOS Games](mobile-support-intro.md)\.

**Topics**
+ [Compiling Shaders for Release Builds](asset-pipeline-shader-compilation.md)
+ [Adding Custom Game Icons](game-build-custom-game-icons.md)
+ [Using the Waf Build System](waf-intro.md)