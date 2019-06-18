# Using AI Bubbles for Error Messaging<a name="ai-debug-bubbles"></a>

The AI Bubbles System is used to collect and display AI agent error messages for level designers\. Debugging wrong behavior for an AI agent can take lots of time as it is difficult to track down which system is connected with the problem and which console variables need to be enabled to retrieve important information\.

Game developers are encouraged to enter important error messages into the AI Bubbles system\.

Error messages can be displayed as speech bubbles above an AI agent, displayed in a pop\-up window, or displayed in the Console window\.

The following console variables are used to control if and how alert messages are displayed:

**ai\_BubblesSystem**  
Enables or disables the AI Bubbles system\.  
Values: `0` =disable \| `1` =enable

**ai\_BubblesSystemDecayTime**  
Specifies the number of seconds a speech bubble remains onscreen before the next bubble is displayed\.  
Units: seconds

**ai\_BubblesSystemAlertnessFilter**  
Specifies the type and level of messages displayed\.  
Values: `0` =none \| `1` =logs \| `2` =bubbles \| `3` =logs and bubbles \| `4` =blocking popups \| `5` =blocking popups and logs \| `6` =blocking popups and bubbles \| `7` =all notifications

**ai\_BubblesSystemUseDepthTest**  
Specifies if the message will be occluded by game objects\.

**ai\_BubblesSystemFontSize**  
Defines the font size of the message displayed\.