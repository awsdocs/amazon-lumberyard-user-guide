# Utilities Nodes<a name="script-canvas-utilities-nodes"></a>

You can use the following utility nodes in the **Script Canvas** editor:

## Clip Capture<a name="script-canvas-clip-capture-node"></a>

Captures video clips while a game is running and saves them locally or to the cloud\. This generally refers to built\-in DVR capabilities of video game consoles\.

**Note**  
Currently, this node supports Xbox One only\.

**Contents**
+ [Inputs](#script-canvas-clip-capture-node-input)
+ [Outputs](#script-canvas-clip-capture-node-output)

![\[clipcapture, clipcapturenode, clipcaptureutilities\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/scriptcanvasnodes/script-canvas-clip-capture-node.png)

### Inputs<a name="script-canvas-clip-capture-node-input"></a>


****  

| Pin | Type | Description | 
| --- | --- | --- | 
| In | Event | Triggers the node\. | 
| Duration Before | Number |  Records the specified number of seconds before the capture was triggered\. Default value: `20`  | 
| Duration After | Number |  Records the specified number of seconds after the capture is triggered\. Default value: `10`  | 
| Clip Name | String | Usage details that are platform specific\. | 
| Localized Clip Name | String | Usage details that are platform specific\. | 
| Metadata | String | \(Optional\) Parameter for tagging clip instances\. | 

### Outputs<a name="script-canvas-clip-capture-node-output"></a>


****  

| Pin | Type | Description | 
| --- | --- | --- | 
| Out | Event | Sends when the node is finished\. | 
| Success | Boolean | If successful, returns true\. | 