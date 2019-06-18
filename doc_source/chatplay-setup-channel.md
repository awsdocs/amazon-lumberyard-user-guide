# Setting up a Twitch ChatPlay Channel<a name="chatplay-setup-channel"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

This topic discusses how to set up and connect to a Twitch channel\. Go to [Twitch Interactive](https://secure.twitch.tv/signup) to set up a new Twitch channel and follow the directions there before starting this procedure\. 

You need Flow Graph logic to connect to your Twitch channel, listen for keywords, and then act on those keywords\.

**To create a flow graph for Twitch ChatPlay**

1. Open the context \(right\-click\) menu for the object in your level and choose **Create Flow Graph**\.

1. In the dialog box, enter a name for the channel and choose **OK**\.

1. In the **Flow Graph Editor**, under **Components**, **NodeClass**, **Game**, drag the **Start** node onto the graph\.

**To connect to a Twitch channel**

1. In the **Flow Graph Editor**, under **Components**, **NodeClass**, **Game**, drag the **Start** node onto the graph\.

1. Under **Components**, drag the **Twitch:ChatPlay:Channel** node onto the graph\.

1. Connect the **output** of the **Game:Start** node to the **Connect** input of the **Twitch:ChatPlay:Channel** node\.

**To disconnect from a Twitch channel**
+ To disconnect a single channel, use the **Disconnect** port on the **Twitch:ChatPlay:Channel** node\.
+ To disconnect from all channels, use the **Twitch:ChatPlay:DisconnectAll** node\.

**Note**  
Channels are automatically disconnected when flow nodes are uninitialized\. This means that disconnection is automatic in most situations without need for further action\.