# Using Console Variables to Set Agent Perception<a name="ai-perception-cvars"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can also use console variables to affect AI agent perception\. Console variables are accessed by clicking the \(**\.\.\.**\) icon in the right\-corner of Lumberyard Editor\. 

Unless otherwise noted, the variable type is Boolean and the default value is 0\.
+ **ai\_IgnorePlayer ** – Determines the degree to which the agent ignores players\. A setting of 1 is the same as 0% perception scale \(agent ignores players\)\.
+ **ai\_IgnoreBulletRainStimulus** – Determines whether AI agents perceive bullets passing near them\.
+ **ai\_IgnoreVisibilityChecks** – Returns certain visibility checks as false\. 
+ **ai\_IgnoreVisualStimulus** – Notifies the Perception Handler to always ignore visual stimulus\.
+ **ai\_IgnoreSoundStimulus** – Determines whether the agent ignores all sounds\. Visual and tactile stimuli are not affected\.
+ **ai\_SoundPerception** – Determines the degree to which the agent can hear sounds\. A setting of 0 causes the agent to ignore all sounds \(useful for debugging purposes when used in conjunction with ai\_DebugDraw\)\. Default value: 1 
+ **ai\_EnablePerceptionStanceVisibleRange** – Determines the maximum perception range for AI based on the player's stance\.
+ **ai\_CrouchVisibleRange ** – Determines the perception range for AI agents when the player is crouching and ai\_EnablePerceptionStanceVisibleRange is enabled\. Default value: 15\.0 
+ **ai\_ProneVisibleRange ** – Determines the perception range for AI agents when the player is prone and ai\_EnablePerceptionStanceVisibleRange is enabled\. Default value: 6\.0 

For the next three variables, if the isAffectedByLight property is true, this determines the scaling factor for the AI agent's visual perception range under the LIGHTSPOT lighting conditions\.
+ **ai\_SightRangeDarkIllumMod** – Has the same effect as the LIGHTSPOT\_DARK anchor type\. Default value: 0\.5 
+ **ai\_SightRangeMediumIllumMod** – Has the same effect as the LIGHTSPOT\_MEDIUM anchor type\. Default value: 0\.8 
+ **ai\_SightRangeSuperDarkIllumMod** – Has the same effect as the LIGHTSPOT\_SUPERDARK anchor type\. Default value: 0\.25 

**To set perception properties using Database View**

1. In Lumberyard Editor, click **Tools**, **Other**, **DataBase View**\.

1. On the **Entity Library** tab, click **Load Library** to select the applicable entity file\.

1. Select the AI entity in the entity tree\.

1. In the center pane, under **Perception**, enable properties and set parameter values as needed\.