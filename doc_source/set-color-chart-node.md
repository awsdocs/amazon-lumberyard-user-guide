# Set Color Chart<a name="set-color-chart-node"></a>

Applies a color chart texture for color grading\.

**Note**  
When you call the node for the first time, you must set a default color chart for the fade to work correctly\. The **Set Color Chart** node uses this color chart as a reference to fade into the next color chart\. If the **Set Color Chart** node doesn't have a default color chart to fade from, the node will immediately fade to the first color chart, regardless of the fade time\.  
For an example script, see [Example Set Color Chart Script](#color-chart-script-example)\.

**Contents**
+ [Inputs](#set-color-chart-node-input)
+ [Creating a Color Chart for Lumberyard](#creating-a-color-chart-for-lumberyard)
  + [Console Variables for Color Charts](#set-color-chart-console-variables)

![\[setcolorchartnode, setcolorchart, colorchart, colorgrading, setcolorgrading\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/script-canvas-set-color-chart-node.png)

## Inputs<a name="set-color-chart-node-input"></a>


****  

| Pin | Type | Description | 
| --- | --- | --- | 
| In | Event | Triggers the node\. | 
| Texture Name | String |  The name of a color chart texture\. For more information, see [Finding the Texture Name](finding-texture-by-names.md)\.  | 
| Fade Time | Number |  Number of seconds to fade into the color grading\.  | 

## Creating a Color Chart for Lumberyard<a name="creating-a-color-chart-for-lumberyard"></a>

You can create a color chart to apply color grading to your project\. A color chart uses a reference image that can be an example image from your game or an image that contains a wide variety of color\. You then modify the image, such as changing the hue, saturation, brightness, and so on\. 

When you specify the color chart file with the **[Set Color Chart](#set-color-chart-node)** node, Lumberyard takes the image and its color chart and applies the color changes to your level\. For example, you can use a color chart with negative saturation to make your game appear dark and muted\. 

**To create a color chart**

1. Make a copy of the color chart file `default_cch.tiff`\. You can find the color chart file in the `lumberyard_version\dev\Engine\EngineAssets\Textures` directory\. 
**Note**  
You must use this exact file so that the Resource Compiler can detect the color chart and use it to process the color charts that you create\.

   The following is an example color chart image:  
![\[Color chart example for Lumberyard.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/set-color-chart.png)

1. Use a reference image that shows a wide range of colors and that has not been color corrected yet, and do the following:
**Note**  
You don't need to use a high resolution or large reference image\.
You can use any image as a reference, such as screenshot from your game\. 

   1. Copy and paste the color chart image into the reference image\.

   1. Flatten all layers for the image\.

   1. Save the image as `filename_cch.tif`, such as `default_startergame_cch.tif`\.
**Note**  
You do not need to include the `_cch` suffix for the image file\.  
**Example default color chart image**  

   The following image is from [Starter Game Sample](sample-level-starter-game.md) and includes the color chart in the bottom right\.  
![\[Color chart example reference for the Set Color Chart node in Script Canvas.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/set-color-chart-reference-image.png)

1. Make a copy of the image and then do the following: 

   1. Modify the image so that it has the color correction that you want\. Avoid extreme color correction changes, which can result in overlapping colors when the scene is processed\.

   1. Save the image as `filename_cch.tif`, such as `saturation_cch.tif`\.   
**Example modified color chart image**  

   The following image lowers the saturation\.  
![\[Color chart example reference with color correction applied for the Set Color Chart node in Script Canvas.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/set-color-chart-reference-image-saturation.png)

1. Move all three files \(`default_cch.tiff` and your color charts\) to your game project directory, such as `lumberyard_version\dev\StarterGame\textures\defaults\`\. 
**Note**  
You use this directory to specify the file path to the color chart file in the **Set Color Chart** node\. For more information, see [Finding the Texture Name](finding-texture-by-names.md)\.

1. To compile your images so that Lumberyard Editor recognizes them as color charts, do one of the following:
   + In Lumberyard Editor, in the **Asset Browser**, navigate to the color chart file and double\-click it\.
   + If you have the RC Shell Commands plugin installed, right\-click the image and choose **RC Compile Image**\.   
![\[Use the Resource Compiler to open the color chart image.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/resource-compiler-open-image.png)
**Note**  
You can install the plugin in Lumberyard Setup Assistant\. For more information, see [Using Lumberyard Setup Assistant to Set Up Your Development Environment](lumberyard-launcher-intro.md)\. 

1. In the Resource Compiler, verify that **ColorChart** is selected, click** Generate Output**, and then click **OK**\.  
![\[Example color chart processed by the Asset Processor.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/set-color-chart-processed.png)
**Note**  
You can clear the **Tiled** option to preview the image correctly\. This option does not affect your color chart\.
To see more information about **ColorChart** settings, click **Show preset info**\. You can find these settings in the `rc.ini` file, located in the `lumberyard_version\dev\Bin64vc140\rc\` directory\.   
For more information, see [Using the Resource Compiler Image Tool](asset-pipeline-images-using-resourcecompiler-image-tool.md)\.

1. Repeat steps 5 and 6 for all your color chart images\.

1. In the **Script Canvas** editor, create a script\. In the **[Set Color Chart](#set-color-chart-node)** nodes, specify the path to the color chart files that you created, and the **Fade Time**\.<a name="color-chart-script-example"></a>  
**Example Set Color Chart Script**  

   The example script does the following:

   1. When the graph starts, the **Set Color Chart** node sets a default color chart with the `default_startergame_cch.tif` file\.

   1. The **Delay** node waits three seconds\.

   1. During the next five seconds, the **Set Color Chart** node fades the screen to the color chart with the `saturation_cch.tif` file\.  
![\[Example Set Color Chart node with the default color chart image specified and the new color chart.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/set-color-chart-on-graph-example.png)

1. Attach the **[Script Canvas](component-script-canvas.md)** component to an entity and specify the script\. For more information, see [Working with Components](component-working.md)\. 

1. To test your script in game mode, press **Ctrl\+G**\.  
**Example**  

   The following example demonstrates the script\.  
![\[Use the Set Color Chart node and set a color chart to modify the color grading in your game project.\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/set-color-chart-node-example.gif)

1. To exit game mode, press **Esc**\.

### Console Variables for Color Charts<a name="set-color-chart-console-variables"></a>

You can use the following console variables for working with color charts\. For more information, see [Using the Console Window](console-intro.md)\.


****  

| Console Variable | Description | Valid Values | 
| --- | --- | --- | 
| r\_ColorGrading |  Enables color grading\.  |  `0` = Off `1` = On \(default\)  | 
| r\_ColorGradingCharts |  Enables color grading with color charts\.  |  `0` = Off `1` = On \(default\)  | 
| r\_ColorGradingChartsCache |  Enables cache updates for the color grading charts\.  |  `0` = Always update\. `1` = Update every other frame\. `2` = Update every two frames\. `3` = Update every three frames\. `4` = Update every four frames \(default\)\.  | 
| r\_ColorGradingFilters | Enables color grading for filters\. |  `0` = Off `1` = On \(default\)  | 
| r\_ColorGradingLevels | Enables color grading for levels\. |  `0` = Off `1` = On \(default\)  | 
| r\_ColorGradingSelectiveColor | Enables color grading for the selected color\. |  `0` = Off `1` = On \(default\)  | 