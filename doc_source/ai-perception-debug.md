# Debugging AI Agent Perception Issues<a name="ai-perception-debug"></a>

For debugging specific AI perception issues, use the following console variables\. To debug generic AI issues, see [AI Agent Debugging](ai-debug-intro.md)\.

Unless otherwise noted, variable type is Boolean and default value is 0\.
+ **ai\_DebugGlobalPerceptionScale** – Displays global perception scale multipliers\.
+ **ai\_DrawPerceptionIndicators** – Displays indicators showing the enemy's current perception level of player\.
+ **ai\_DrawPerceptionDebugging** \- Displays indicators showing how the enemy view intersects with perception modifiers\. 
+ **ai\_DrawPerceptionModifiers** \- Displays perception modifier areas in game mode\.
+ **ai\_DrawPerceptionHandlerModifiers** – Displays perception handler modifiers on a specific AI agent\. Requires an AIName as the parameter\.
+ **ai\_DebugPerceptionManager** – Displays perception manager performance overlay\. 
+ **ai\_DebugDrawLightLevel ** – Displays the AI light level\. Useful for debugging with lightspot anchors\. 
+ **ai\_DrawAgentFOV** – Displays the FOV cone for AI agents\. Requires ai\_DebugDraw to be enabled\. 
+ **ai\_DrawAgentStats** – Displays information about agents\. Nadlt=name/alertness/distances/light level/target\. 
+ **ai\_DrawAttentionTargetPositions ** – Displays position markers for the AI agent's current attention target\. 