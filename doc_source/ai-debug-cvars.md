# Using AI Debug Console Variables<a name="ai-debug-cvars"></a>

There are a number of console variables available for AI agent debugging\. One of the most useful is the **ai\_DebugDraw** console variable\. Setting this variable to `1` results in debug information displayed above any active AI agent\.

**Note**  
Use the **ai\_AgentStatsDist** variable listed below to set the distance above the AI agent that debug information displays\.

**To enable ai\_DebugDraw**

1. Open Lumberyard Editor and select **Tools**, **Console**\.

1. At the bottom of the console window, enter **ai\_DebugDraw 1** or one of the other values, as needed:


**ai\_DebugDraw Values**  

| Value | Description | 
| --- | --- | 
| \-1 | Only warnings and errors; no other information displays  | 
| 0 | Disables AI debug draw | 
| 1 | Standard AI debug draw information displays | 
| 71 | Draws all forbidden areas \(including auto\-generated ones\) | 
| 72 | Draws graph errors \(problematic areas are highlighted with circles\) | 
| 74 | Draws the whole navigation graph | 
| 79 | Draws the navigation graph close to the player \(within 15m from the camera; faster than 74\) | 
| 80 | Draws tagged nodes \(during A\*\) | 
| 81 | Calculates \(if necessary\) and then draws 3D \(volume\) hidespots | 
| 82 | Draws 3D \(volume\) hidespots | 
| 85 | Draws steep slopes \(determined by ai\_steep\_slope\_up\_value and ai\_steep\_slope\_across\_value\) | 
| 90 | Draws flight navigation within a 200m range of the player | 
| 179 | Similar to 79, but also shows triangulation edges centers | 
| 279 | Similar to 179, but also shows water depth information | 
| 1017 | Visualizes navigation links of node that encloses entity "test" | 

## Setting AI\_DebugDraw to 1<a name="ai-debug-cvars-debugdraw"></a>

Setting **ai\_DebugDraw **to `1` enables the following console variables for debugging:

**ai\_AllTime**  
Displays the update times of all agents in milliseconds\. Green indicates <1ms and white indicates 1ms\-5ms\.  
Values: `0` = Disabled \| `1` = Enabled

**ai\_DebugDrawNavigation 1**  
Displays the navigation mesh for the MNM system\. Blue areas are navigable for AI agents to move around in\. Red areas are cut off from the main mesh and are not reachable by AI agents\.  
Values: `0` = Disabled \| `1` = Triangles and contour \| `2` = Triangles, mesh, and contours \| `3` = Triangles, mesh contours, and external links

**ai\_DrawBadAnchors**  
Toggles drawing out\-of\-bounds AI objects of a particular type for debugging AI\. Valid only for 3D navigation\. Draws red spheres at positions of anchors that are located out of navigation volumes\. Those anchors must be moved\.   
Values: `0` = Disabled \| `1` = Enabled

**ai\_DrawFormations**  
Draws all the currently active formations of the AI agents\.  
Values: `0` = Disabled \| `1` = Enabled

**ai\_DrawModifiers**  
Toggles the AI debugging view of navigation modifiers\.

**ai\_DrawNode**  
Toggles the visibility of named agent's position on AI triangulation\. See also: ai\_DrawNodeLinkType and ai\_DrawNodeLinkCutoff\.   
Values: `none` = Disabled \| `all` = Displays all agent nodes \| `player` = Displays the player node \| `agent name` = Displays the agent node

**ai\_DrawNodeLinkType**  
Sets the link parameter to draw with ai\_DrawNode\.  
Values: `0` = Pass radius \| `1` = Exposure \| `2` = Maximum water depth \| `3` = Minimum water depth

**ai\_DrawNodeLinkCutoff**  
Sets the link cutoff value in ai\_DrawNodeLinkType\. If the link value is more than ai\_DrawNodeLinkCutoff, the number displays in green\. If the link value is less than ai\_DrawNodeLinkCutoff, the number displays in red\. 

**ai\_DrawOffset**  
Vertical offset during debug drawing\.

**ai\_DrawPath**  
Draws the generated paths of the AI agents\. ai\_drawoffset is used\.  
Values: `none` = Disabled \| `squad` = Squad members \| `enemy` = Enemies \| `groupID` = Group members

**ai\_DrawRadar**  
Draws a radar overlay at the center of the view\.   
Values: `0` = Disabled \| `value` = size of radar \(m\)

**ai\_DrawRadarDist**  
AI radar draw distance in meters\.  
Default value: `20m`

**ai\_DrawRefPoints**  
Toggles reference points and beacon view for debugging AI\. Draws balls at AI reference points\.  
Usage: `"all", agent name, group id `

**ai\_DrawStats**  
Toggles drawing stats \(in a table on top left of screen\) for AI objects within a specified range\. Displays attention target, goal pipe, and current goal\. 

**ai\_StatsDisplayMode 1**  
Displays information on the number of active AI agents, full AI updates per frame, and the number of TPS queries processed each frame\. 

**ai\_DrawTargets**  
Distance to display the perception events of all enabled puppets\. Displays target type and priority\. 

**ai\_DrawType**  
Displays all AI object of a specified type\. If object is enabled, it displays with a blue ball\. If object is disabled, it displays with a red ball\. A yellow line represents forward direction of the object\.   
Values: `<0` = Disabled \| `0` = Displays dummy objects \| `>0` = Object type to display

**ai\_DrawTrajectory**  
Records and draws the actual path taken by the agent specified in ai\_StatsTarget\. The path displays in the color aqua, and only a certain length displays\. The old path gradually disappears as a new path is drawn\.   
Values: `0` = Disable \| `1` = Enabled

**ai\_DebugTacticalPoints**  
Displays debugging information on tactical point selection system \(TPS\)\.

**ai\_Locate**  
Indicates the position and some base states of specified objects\. Pinpoints the position of the agents; its name; its attention target; draw red cone if the agent is allowed to fire; draw purple cone if agent is pressing trigger\.   
Values: `none` = Disabled \| `squad` = Squad members \| `enemy` = Enemies \| `groupID` = Group members

**ai\_ProfileGoals**  
Records the time used for each AI goal \(approach, run, pathfind\) to execute\. The longest execution time displays onscreen\.   
Default value: `0` = Disabled

**ai\_StatsDisplayMode**  
Gives information on the number of active AIs, full updates, and TPS queries for every frame\.  
Values: `0` = Hide \| `1` = Display

**ai\_StatsTarget**  
Displays the current goal pipe, current goal, subpipes, and agent stats information for the selected AI agent\. A long, green line represents the AI forward direction\. A long, red or blue line represents the AI view direction if the AI is firing or not firing\.   
Values: `AI name`

**ai\_SteepSlopeAcrossValue**  
Indicates the maximum slope value that is borderline walkable across the slope\. Zero \(0\.0\) value indicates flat \(no slope\)\. Must be set to a value greater than ai\_SteepSlopeUpValue\.  
Default value: `0.6`

**ai\_SteepSlopeUpValue**  
Indicates the maximum slope value that is borderline walkable up the slope\. Zero \(0\.0\) value indicates flat \(no slope\)\. Must be set to a value smaller than ai\_SteepSlopeAcrossValue\.  
Default value: `1.0`

## Other AI\_Debug Variables<a name="ai-debug-cvars-other"></a>

There are a number of other `ai_DebugDraw` console variables that can be accessed\. Click the \(**\.\.\.**\) icon at the bottom right corner of the console, and then enter **ai\_debug** in **Search**\.