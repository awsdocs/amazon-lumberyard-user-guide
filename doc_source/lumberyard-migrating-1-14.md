# Lumberyard 1\.14<a name="lumberyard-migrating-1-14"></a>

Use the following instructions if you are upgrading your projects to Lumberyard 1\.14\.

## Converting Script Canvas Scripts<a name="lumberyard-migrating-1-14-converting-script-canvas-scripts"></a>

Lumberyard 1\.14 introduces changes to Script Canvas that affect scripts created in Lumberyard 1\.13 and earlier\.

The following changes to Script Canvas were made for Lumberyard 1\.14:
+ Variables are now created and defined in a **Variable Manager** window\. You can also create get and set nodes from this window by doing any of the following:
  + Drag the variable into the canvas and then choose **Get** or **Set**\.
  + Press **Shift** and drag the variable into the canvas to create a get node\.
  + Press **Alt** and drag the variable into the canvas to create a set node\.

  Variables for existing graphs appear in the **Variable Manager** window\.
+ The **Get Variable** node now has an execution trigger\. One or more new **Get Variable** nodes will replace existing **Get Variable** nodes, and the new **Get Variable** nodes will be spliced into the execution of the graph\. If a single **Get Variable** node connects to two different nodes, a duplicate **Get Variable** node will be automatically created adjacent to the original **Get Variable** node\. The duplicate node will be spliced into the alternate execution connection\.
+ Script Canvas file sizes have been reduced\.

You have two options to convert your scripts:
+ Open each script file \(`.scriptcanvas`\) to convert the script automatically\.
+ Use the batch conversion tool to convert a specified directory and all child script files \(`.scriptcanvas`\)\.

## Using the Batch Conversion Tool<a name="lumberyard-migrating-1-14-using-batch-conversion-tool"></a>

Rather than converting each Script Canvas script individually, you can use the batch conversion tool to convert all `.scriptcanvas` files that are located in a specified directory and its child directories\.

**Note**  
The **Script Canvas** editor must remain the active window while the batch conversion tool processes files\. If you need the editor to run in the background, you can set the `ed_KeepEditorActive` console variable to **1**\.

**To convert Script Canvas graphs using the batch conversion tool**

1. In the **Script Canvas** editor, choose **File**, **Edit**, **Batch Conversion**\.

1. In the **Select Folder** window, do one of the following:
   + Select an individual folder to convert only the `.scriptcanvas` files in that folder\.
   + Select a parent directory to convert all `.scriptcanvas` files in all subfolders\.

1. Click **Select Folder**\.

   When the conversion process is finished, the batch conversion tool automatically closes\.