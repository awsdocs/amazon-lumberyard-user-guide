# Managing Track Events<a name="cinematics-tracks-events-intro"></a>

A track event is a trigger that allows you to integrate Flow Graph logic with a track view scene\. When a track event is triggered from the scene, its corresponding output in a Flow Graph node is activated\. A scene can contain a number of track events that are grouped under a Track Event Node\. Each track event can have multiple keys assigned to it\.

Track events can also be used to change the time of day in terrain level\.

**To add a track event**

1. In the **Track View** editor, right\-click the applicable scene\. Click **Edit Events**\.

1. Click **Add**, and then enter a name\. Close the dialog\.

1. Under the track event node, click the **Track Event** track, then double\-click to place a key in the timeline row adjacent to it\.

1. In **Key Properties**/**Value**, enter a value\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cinematics-track-events-fg.png)

## Linking Track View Events with Flow Graph<a name="cinematics-tracks-events-fg"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

The track events you create in the **Track View** editor can be used in Flow Graph by adding a Track Event node in Flow Graph and setting its **Sequence** property to the track view sequence triggering the event\. The Track Event Flow Graph node has outputs for each event in that sequence\.

Certain features required for creating cinematic effects are available only in Flow Graph\. To access these features, you need a link between the **Track View** editor and Flow Graph\. Specifically, track view trigger entities are used to send events to Flow Graph where various nodes are then triggered\.

Use the following procedure to create your link between track view sequence and flow graph after you have created an event and assigned it to the key, as described in the previous section\.

**To place the TrackEvent node in flow graph and link it to the event node**

1. Open Flow Graph Editor\.

1. Open a new or existing flow graph\. Right\-click in the flow graph and click **Add Track Event Node** in the context menu\.

1. Double\-click the **Sequence=** box\. Click **\.\.** to open the **Select Sequence** dialog\.

1. Select the track view sequence that your event is coming from\.

   Your **TrackEvent** node's output port is now labeled with your track view event name\.

   The output port activates when the sequence key is reached\. You could then wire this port to a node that will be activated at that point in the sequence\.