# Using the Track View Editor<a name="cinematics-track-view-editor"></a>

The **Track View** editor is the primary tool to create and manage cinematic sequences or animation keyed events\. Whether you want to generate cutscenes for games or create a script to trigger an animation, you can use the **Track View** editor to control cameras, component entities, global variables within a level, and so on\. 

**To open the **Track View** editor**
+ Do one of the following:
  + In Lumberyard Editor, choose **Tools**, **Track View**\.
  + Press the shortcut **T**\.

A *[sequence](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#sequence)* is a term that refers to the content generated from the **Track View** editor for cutscenes or other canned animation triggers\. When you create a sequence, this creates a component entity within the level that stores all of the animation key data that you specified in the **Track View** editor\.

**To create a sequence**

1. In the **Track View** editor, do one of the following: 

   1. Choose **Sequences**, **New Sequence**\.

   1. Click the **Add Sequence** icon ![\[Add track view sequence icon\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cinematics-track-view-simple-motion-component-2.png)\.

1. Enter a sequence name and click **OK**\.

1. In the **Entity Outliner**, a component entity appears with the same name as your created sequence\. This component entity has a **Sequence** component, which stores your sequence data from the **Track View** editor\.

Anything part of the sequence is considered a *node*\. Nodes can be a reference to existing component entities or added to a sequence such as a **Director** node\. 

Each node can have one or more tracks, depending on what you want to animate\. A *track* is what displays animation keys on a timeline in relation to the property that is animated on a node\.

For more information, see [Track View Editor Nodes](cinematics-trackview-nodes.md)\.

**Topics**
+ [Track View Editor Toolbars](cinematics-track-view-editor-toolbars.md)
+ [Track View Editor Nodes](cinematics-trackview-nodes.md)
+ [Adding and Removing Animation Keys on Tracks](adding-removing-animation-keys-on-tracks.md)
+ [Controlling the Playhead](cinematics-controlling-the-playhead.md)
+ [Using Record Mode](cinematics-using-record-mode.md)
+ [Using Animation Curves](cinematics-track-view-editor-animation-curves.md)