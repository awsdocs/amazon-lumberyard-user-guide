# Transform2D – Managing UI Anchors and Offsets<a name="ui-editor-anchors"></a>

You can use anchors and offset settings in the **Transform2D** component to set a UI element's position and size relative to its parent's edges\. The **Transform2D** component is a required component in every element\.

Anchor values are always `0.00%` to `100.00%` as defined by the parent's edges\. Offsets are expressed in pixels and are relative to the anchors\.

Anchors and offsets are useful in a variety of situations:
+ Ensuring an element maintains a specific padding within its parent's edges, regardless of changes to the parent's size
+ Anchoring an element to a corner of its parent, regardless of changes to the parent's size or position
+ Building resolution\-independent UI elements

For example, you can ensure an element remains full screen regardless of the screen's resolution\.

**To configure an element's anchors**

1. In the **Hierarchy** pane of the [**UI Editor**](ui-editor-using.md), select the element whose anchors you want to modify\.

1. In the **Properties** pane, under **Transform2D**, choose from the selection of commonly used anchor placements\.

   1. Anchor to the parent's center, corner, or midway along an edge without changing size\.

       

   1. Anchor to the left edge, middle, or right edge; vertical size adjusts to parent\.

       

   1. Anchor to the top edge, middle, or bottom edge; horizontal size adjusts to parent\.

       

   1. Anchor all of the element's edges to the parent; horizontal and vertical size adjusts to parent\. You can use this anchor preset to place an element that remains full screen, regardless of a change in resolution \(if the canvas is its parent\)\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/ui-editor-presets-1.png)

**To further edit \(fine\-tune\) an element's anchors**  
In the **Properties** pane, under **Transform2D**, do the following for **Anchors**, as appropriate:  
+ For **Left**, enter a value between `0.00%` and `100.00%`\.
+ For **Right**, enter a value between `0.00%` and `100.00%`\.
+ For **Top**, enter a value between `0.00%` and `100.00%`\.
+ For **Bottom**, enter a value between `0.00%` and `100.00%`\.

The anchors' positions can be visualized as points on a grid, plotted in percentages by the length of its parent's edges from left to right and top to bottom\. If you want to keep the element's size absolute \(so that it doesn't change size when the parent changes size\) but want to anchor it a particular vertical or horizontal point relative to the parent's size, make sure the top and bottom \(or left and right\) anchors have the same number\. In this case, the anchors are said to be together\.

But if, for example, you want the element's left and right edges to each remain at a fixed percentage relative to its parent and to change size as its parent changes size, then make the numbers different\. In this case, the anchors are called split\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/ui-editor-percent.png)

**To edit an element's position and size**  
In the **Properties** pane, under **Transform2D**, modify the **Offsets**, as appropriate:  
If the element's anchors are together, do the following:  
+ For **X Pos**, enter a negative or positive value in pixels\. This adjusts the horizontal offset relative to the left\-right anchor position\. 
+ For **Y Pos**, enter a negative or positive value in pixels\. This adjusts the vertical offset relative to the top\-bottom anchor position\.
When the element's anchors are together, only its position \(and not its size\) adjusts with the parent's size\. Therefore, you can manually adjust its size, which remains consistent when anchors are together:  
+ For **Width**, enter a value in pixels\.
+ For **Height**, enter a value in pixels\.
If the element's anchors are split, do the following:  
+ For **Left**, enter a negative or positive value in pixels\. This adjusts the size offset relative to the element's left anchor\.
+ For **Right**, enter a negative or positive value in pixels\. This adjusts the size offset relative to the element's right anchor\.
+ For **Top**, enter a negative or positive value in pixels\. This adjusts the size offset relative to the element's top anchor\.
+ For **Bottom**, enter a negative or positive value in pixels\. This adjusts the size offset relative to the element's bottom anchor\.

**To edit an element's pivot, rotation, and scale**  
In the **Properties** pane, under **Transform2D**, do the following for **Pivot**, **Rotation**, and **Scale**, as appropriate:  
+ For **Pivot**, select a pivot preset or enter values for X and Y where `0` and `1` represent the element's edges\.
+ For **Rotation**, enter a value in degrees\.
+ For **X Scale**, enter a value to use as a multiplier for the element's width\.
+ For **Y Scale**, enter a value to use as a multiplier for the element's height\.
+ Select **Scale to Device** if you want the UI element and its children to scale with the device resolution\.

**Note**  
The element rotates around, resizes from, and calculates position from its pivot point\. The pivot point is not limited by the element's borders; you can place the pivot outside of the element\.