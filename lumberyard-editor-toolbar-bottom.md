# Using the Bottom Toolbar<a name="lumberyard-editor-toolbar-bottom"></a>

 Lumberyard Editor includes a bottom toolbar that provides status as well as the features below\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/editor-toolbar-bottom.png)

## Status<a name="lumberyard-editor-toolbar-bottom-status"></a>

The **status** bar \(A\) displays the number of selected object\(s\) and provides functional hints for buttons or menu items in Lumberyard Editor\.

## Lock Selection<a name="lumberyard-editor-toolbar-bottom-lock"></a>

The **Lock Selection** button \(B\) toggles selection locking, preventing you from inadvertently selecting something else in a level\.

When your selection is locked, you can click or drag the mouse anywhere in the viewport without losing your selection\. To deselect or alter your selection, click **Lock Selection** again to unlock the selection\.

## Coordinates/Transforms<a name="lumberyard-editor-toolbar-bottom-coordinates"></a>

The **coordinates/transform** area \(C\) shows the position of the cursor or the status of a transform, and allows you to enter new transform values\. The information in these fields vary based on your tasks:
+ When creating an object or moving the mouse in the viewport, these fields show the cursor location in absolute world coordinates\.
+ When transforming an object by dragging it in the viewport, these fields show coordinates relative to the object's coordinates before the transformation started\.
+ While transforming an object, these fields change to spinners in which you can directly type values\.
+ When the transform button is active and a single object is selected, but you are not dragging the object, these fields show the absolute coordinates for the current transform\.
+ While the transform button is active and multiple objects are selected, these fields show the previous selection's transform coordinates\.

## Set Vector<a name="lumberyard-editor-toolbar-bottom-vector"></a>

The **Set Vector** button \(D\) allows you to set the vector scale for your selected object\(s\)\. You can lock the proportions by clicking the lock button\.

## Speed Control<a name="lumberyard-editor-toolbar-bottom-speed"></a>

The **Speed** button \(E\) allows you to change the speed of all movements in the viewport\. The three buttons to the right of the **Speed** change the speed to 0\.1, 1, or 10\. You can also manually set the speed by entering your values into the fields or using the spinners to adjust the speed up or down\.

## Terrain Collision<a name="lumberyard-editor-toolbar-bottom-terrain-collision"></a>

The **Terrain Collision** button \(F\) toggles terrain collision\. You can enable terrain collision to inhibit camera movement below the terrain surface\.

## AI/Physics<a name="lumberyard-editor-toolbar-bottom-ai"></a>

The **AI/Physics** button \(G\) toggles physics simulation and AI, allowing you to test physics and AI behavior directly in the editor without entering game mode\.

## No Sync Player<a name="lumberyard-editor-toolbar-bottom-no-sync"></a>

The **No Sync Player** button \(H\) detaches the player entity from the camera\. While in editor mode, a character entity is attached to the camera that is otherwise always synchronized\. The No Sync Player function can be useful with AI or Physics enabled, when you don't want to activate triggers while navigating through a level\.

## Goto Position<a name="lumberyard-editor-toolbar-bottom-goto"></a>

The **Goto Position** button \(I\) opens the **Go to position** dialog box to jump to a specific location in the level\. You can enter positional coordinates or use the spinners to specify values\. If you click the **Go To** button, you immediately move the viewport to the specified coordinate\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/editor-toolbar-bottom-goto.png)

## Mute Audio<a name="lumberyard-editor-toolbar-bottom-audio"></a>

The **Mute Audio** button \(J\) mutes audio and all sounds in the level\.

## VR Preview<a name="lumberyard-editor-toolbar-bottom-vr"></a>

The **VR Preview** button \(K\) previews your game project in [virtual reality mode](virtual-reality-preview.md) when a [virtual reality](virtual-reality.md) gem is enabled\.