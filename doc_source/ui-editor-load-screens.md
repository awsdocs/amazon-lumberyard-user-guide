# Defining Game and Level Load Screens<a name="ui-editor-load-screens"></a>

You can create a game or level loading screen with the **UI Editor**\. The game loading screen is displayed while the game loads\. The level loading screen is displayed while a level loads\. You can create and define a loading screen for each level\.

To define the game and level loading screens, you set the file paths as parameters in `game.cfg` and `level.cfg`\. Alternatively, you can use **Flow Graph** to specify a level loading screen\.

## Defining a Game Loading Screen<a name="ui-editor-load-screens-game"></a>

To define a game loading screen, you first create the loading screen canvas in the **UI Editor** and save it in your project directory\. For example, the Samples Project directory is `lumberyard_version\dev\SamplesProject\`\. You then add or modify parameters in `game.cfg`, which is at the root of your project directory\.

**To add game loading screen parameters to `game.cfg`**

1. In a text editor, open `game.cfg` at the root of your project directory\.

1. Add or modify the following parameters in `game.cfg`:
   + `game_load_screen_uicanvas_path` – File path to the `.uicanvas` game load screen file relative to your project path\.  
**Example**  

     If your game load canvas is at `lumberyard_version\dev\SamplesProject\UI\Canvases\UiAnimMultiSequence.uicanvas`, you would specify the following path:

     `\UI\Canvases\UiAnimMultiSequence.uicanvas`
   + `game_load_screen_sequence_to_auto_play` – Name of the game load screen animation sequence to play on load\.
   + `game_load_screen_sequence_fix_fps` – A fixed frame rate for the game load screen animation to play on load\. Default is `60`\. To ignore this setting and use the real time\-delta, specify `-1`\.

The following is an example of these parameters in a `game.cfg` file:

```
game_load_screen_uicanvas_path="UI\Canvases\UiAnimMultiSequence.uicanvas"
game_load_screen_sequence_to_auto_play="TopRowMove"
game_load_screen_sequence_fix_fps=4.0
```

## Defining a Level Loading Screen<a name="ui-editor-load-screens-level"></a>

To define a level loading screen, you first create the loading screen canvas in the **UI Editor** and save it in that level's directory\. You then add or modify parameters in `level.cfg`, which is at the root of your level directory\.

**To add level loading screen parameters to `level.cfg`**

1. In a text editor, open `level.cfg` at the root of your level directory\.

1. Add or modify the following parameters in `level.cfg`:
   + `level_load_screen_uicanvas_path` – File path to the `.uicanvas` level load screen file relative to your project path\.   
**Example**  

     If your level load canvas is at `lumberyard_version\dev\StarterGame\Levels\StarterGame\UiAnimMultiSequence.uicanvas` \(root of the level directory, which is the same as `level.cfg`\), specify the following path:

     `Levels\StarterGame\UiAnimMultiSequence.uicanvas`
   + `level_load_screen_sequence_to_auto_play` – The name of the level load screen animation sequence to play on load\.
   + `level_load_screen_sequence_fix_fps` – A fixed frame rate for the level load screen animation to play on load\. Default is `60`\. To ignore this setting and use the real time\-delta, specify `-1`\.

The following is an example of these parameters in a `level.cfg` file:

```
level_load_screen_uicanvas_path="Levels\StarterGame\UiAnimMultiSequence.uicanvas"
level_load_screen_sequence_to_auto_play="TopRowMove"
level_load_screen_sequence_fix_fps=4.0
```

### Specifying a Level Loading Screen with Flow Graph<a name="ui-editor-load-screens-level-flowgraph"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can also specify a level loading screen using **Flow Graph** by using the **Mission:LoadNextLevel** node\.

**To specify a level loading screen with Flow Graph**
+ In Flow Graph, open a level flow graph\. Add the **Mission:LoadNextLevel** node\.

  Define the following parameters:
  + `LoadScreenUiCanvasPath` – File path to the `.uicanvas` level load screen file relative to your project path\.   
**Example**  

    If your level load canvas is at `lumberyard_version\dev\StarterGame\Levels\StarterGame\UiAnimMultiSequence.uicanvas` \(root of the level directory, which is the same as `level.cfg`\), specify the following path:

    `Levels\StarterGame\UiAnimMultiSequence.uicanvas`
  + `LoadScreenSequenceToAutoPlay` – Name of the level load screen animation sequence to play on load\.
  + `LoadScreenSequenceFixFps` – A fixed frame rate for the level load screen animation to play on load\. Default is `60`\. To ignore this setting and use the real time\-delta, specify `-1`\.