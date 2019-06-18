# Using AI Anchors to Set Agent Perception<a name="ai-perception-rb"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

Another way to control AI agent perception is to use AI anchors\. Unlike the Flow Graph method, which relies on logic, this method relies on object placement and level markup\.

There are four AI anchors for controlling an AI agent's perception: LIGHTSPOT\_LIGHT, LIGHTSPOT\_MEDIUM, LIGHTSPOT\_DARK, and LIGHTSPOT\_SUPERDARK\. As you might expect, LIGHTSPOT\_SUPERDARK gives an agent the least amount of perception\.

These settings limit the visibility for the AI agent inside the specified radius\. If a player is inside this radius, the agent has a diminished perception of the player\.

**Note**  
To reduce demands on performance, use these AI anchors in place of visual light entities or the sun\.

**To use AI Anchors for setting perception**

1. In the **Rollup Bar**, on the **Objects** tab, click **AI, AIAnchor**\.

1. Under **AIAnchor Properties**, double\-click **AnchorType**\.

1. In **AI Anchors**, select one of the four anchors\.

1. Select **Enabled**\.

1. Click **radius** and enter a value in meters\.