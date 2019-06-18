# Using Auto Disable for Agents<a name="ai-perception-auto-disable"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

You can save processor time by not updating distant AI agents\. To control this on a global and on a per\-agent basis, enable the **AutoDisable** property\.

**To enable AutoDisable using the Rollup Bar**

1. In the Rollup Bar, on the **Objects** tab, click **Entity** and select your asset\.

1. Under **Entity Properties2**, select the **AutoDisable** check box\.

**To enable AutoDisable using Flow Graph**

1. In Lumberyard Editor, click **Tools**, **Flow Graph**\.

1. Under **Flow Graphs**, select your asset\.

1. Right\-click anywhere in the graph and then click **Add Node, AI, AutoDisable**\.

1. In the **AI:AutoDisable** node, click **ON** to enable **AutoDisable**\.

**Note**  
You can also enable **AutoDisable** by setting the console variable **ai\_UpdateAllAlways** value to 0\.