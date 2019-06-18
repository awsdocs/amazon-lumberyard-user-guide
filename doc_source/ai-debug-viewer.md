# Using the AI Debug Viewer<a name="ai-debug-viewer"></a>

AI Debug Viewer is the viewing utility that loads, parses, and displays the AI Debug Recorder file\. This utility is accessed from Lumberyard Editor\.

**To view a AI Debug Recorder session**

1. In Lumberyard Editor, click **Tools**, **Other**, **AI Debugger**\.

1. In AI Debugger, click **File**, **Load** to view the last recorded session, or click **Load As** to view a prior pre\-recorded session\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/ai-debug-viewer.png)

The timeline window can be broken down as shown below:

**1\. Stream Window**\. Displays the contents of all active streams for all of the AI agents who were recorded, along the timeline\. By right\-clicking in this window, a context menu is displayed, as follows:


**Context Menu Items**  

| Menu Item | Description | 
| --- | --- | 
| Copy Label | Copies the current label of the stream to the clipboard\. See the Info Window for more details\. | 
| Find\.\.\. | Finds the next occurrence of the label you specify along the timeline and sets the cursor to that point\. | 
| Goto Start | Sets the cursor to the starting time of the recording\. | 
| Goto End | Sets the cursor to the ending time of the recording\. | 
| Goto Agent Location | Sets the position of the camera in the Editor to the location of the agent who owns the stream\. | 
| Copy Agent Location | Copies the location of the agent who owns the stream to the clipboard\. | 
| Following Content | Contains all of the available streams for viewing\. The check box next to the name of the stream means it is enabled\. Enabling a stream causes its contents to be displayed in the Stream window\. | 

**2\. Agent Window**\. Displays the name of the agent who owns the contents of the stream\. Right\-clicking this window displays the context menu, as follows:
+ **Enable Debug Drawing** \- Select to active debugging for this agent\.
+ **Set Editor View** \- Select to focus the Editor’s camera as centered on both the position and facing direction of the AI agent based on where the cursor is currently set\. This allows you to see what that AI agent was seeing at any moment in time\. By moving the cursor, you can replay the agent's movements and see what it was seeing\.
+ **Set Color** \- Change the debug color used for representing this agent's information\.

**3\. Info Window**\. Displays the last value of the stream based on the cursor position for the stream to the left\. The references to **label** in various places throughout the debug viewer refer to the text you see in this pane\.

**4\. Ruler Window**\. Displays the current time and can be used to select time ranges or manipulate the cursor\.

The **cursor** is represented by a solid red line\. Any information that occurred at the moment of time depicted by the cursor\.

The **time range** is represented by a blue box\. Click and hold anywhere in the ruler window to drag the time range box\. Releasing the mouse button sets the time range box\. All information that occurred during the highlighted time is drawn\.

**5\. Menu Window**\. Contains configuration and command settings for the view pane\.