# Configuring Canvas Properties<a name="ui-editor-canvas-properties"></a>

The canvas properties are displayed in the **UI Editor** **Properties** pane when no elements are selected\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/ui-editor-canvas-properties.png)

## Rendering Properties<a name="rendering-properties"></a>

The **Is pixel aligned** property, selected by default, makes textures look sharper by rounding to the nearest exact pixel the position of the elements' corners\. For example, if, at a particular screen resolution, the position of a corner of an element rectangle is at 123\.45, 678\.90, then it will be rounded to 123\.00, 679\.00\.

The **Render to texture** property, when selected, causes the UI canvas to be drawn to a texture rather than to the screen\. Selecting this property prompts you to enter a **Render target name** for the texture\. You can enter any name, but the convention is to prefix the name with the **$** symbol to distinguish it from texture assets\.

## Input Properties<a name="input-properties"></a>

The **Handle positional** property, selected by default, causes automatic response to positional input such as mouse movement, mouse button clicks, and touch screen input, as well as keyboard input when an interactive UI element is active \(such as an element with a **Text Input** component on it\)\.

You can de\-select this property for canvases that don't require input\. Another scenario where you may want to de\-select this property is if you configure your game to handle all inputs and then pass selected inputs to the UI system\.

The **Handle navigation** property, when selected, causes automatic response to navigation input\. For example, on a PC, pressing arrow keys will move focus from one interactive UI element to the next, and pressing **Enter** will activate an interactive UI element\. We recommend de\-selecting this property for canvases placed in the game world\.

The **First focus element** property is displayed when **Handle navigation** is selected\. **First focus element** specifies which element gains focus when a canvas is first loaded and a mouse is not detected\. For more information about element navigation, see [First Focus Element](ui-editor-components-firstfocus.md)\.

## Tooltips Properties<a name="editor-properties-tooltips"></a>

The **Tooltips** property controls which element is displayed when hovering over an interactive element\. Select an element from the drop\-down list\. This list is composed of the elements on your current canvas that contain the **TooltipDisplay** component\. For more information about the **Tooltips** components, see [Tooltip Components](ui-editor-components-tooltips.md)\.

## Editor Settings Properties<a name="editor-properties-group"></a>

The **Snap distance** property controls the distance between positions on the grid when **Snap to grid** is selected in the toolbar\.

The **Snap rotation** property specifies the number of degrees between each step of rotation when using the rotation gizmo to rotate an element in the viewport when **Snap to grid** is selected in the toolbar\.