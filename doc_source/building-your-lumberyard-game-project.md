# Building Your Game Project<a name="building-your-lumberyard-game-project"></a>

After you make changes to your game project, such as enabling gems with code and assets, you need to build your game project with the [Lmbr\.exe](lmbr-exe.md)\.

**To build your game project**

1. Open a command line window and navigate to the `lumberyard_version\dev` directory\.

1. Enter the following command:

   ```
   lmbr_waf configure
   ```

1. If the previous step was successful, enter the following build command for your game project, with your version of Visual Studio:

   ```
   lmbr_waf build_win_x64_vs2015_profile -p game
   ```

   For more information about other build commands or variables, see [Build Configuration](waf-commands.md#build-configuration) and [Creating Game Builds](game-build-intro.md)\.

1. After the previous command was successful, start Lumberyard Editor\.