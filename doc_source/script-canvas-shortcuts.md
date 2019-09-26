# Script Canvas Editor Shortcuts<a name="script-canvas-shortcuts"></a>

The following table shows the keyboard shortcuts that you can use in the Script Canvas editor\.


****  

| Key Combination | Action | Description | 
| --- | --- | --- | 
| Arrow Keys | Scroll graph | Depending on the key pressed, scrolls the graph left, right, up, or down\. | 
| Ctrl\+C | Copy | Copies to the clipboard selected nodes and the connections between them\. | 
| Ctrl\+V | Paste | Attempts to paste nodes and connections that have been copied to the clipboard into the active graph\. | 
| Ctrl\+D | Duplicate | Duplicates the currently selected nodes in the active graph\. This is the equivalent of using Ctrl\+C and Ctrl\+V\. | 
| Ctrl\+Left Arrow | Select inputs | Selects all the nodes that are connected to the current selection through input connections\. | 
| Ctrl\+Right Arrow | Select outputs | Selects all the nodes that are connected to the current selection through output connections\. | 
| Ctrl\+Up Arrow | Select connected nodes | Selects all the nodes that are connected to the current selection through any connection\. | 
| ESC | Clear selection | Removes the selection of all currently selected nodes\. | 
| Ctrl\+Shift\+P | Screenshot graph | Creates an image of the active graph and adds it to the clipboard\. Creates a screenshot of a selected area only if nodes are selected at the time the action is taken\. | 
| Shift\+Left Arrow | Align left | Aligns all the currently selected nodes to the left\. | 
| Shift\+Right Arrow | Align right | Aligns all the currently selected nodes to the right\. | 
| Shift\+Up Arrow | Align top | Aligns all the currently selected nodes to the top\. | 
| Shift\+Down Arrow | Align bottom | Aligns all the currently selected nodes to the bottom\. | 
| Ctrl\+Alt\+M | Add comment | Adds the default comment preset to the active graph\. For information about presets, see [Comment and Group Presets](script-canvas-comment-and-group-presets.md)\. | 
| Ctrl\+Shift\+G | Group selection | Groups the current selection on the graph using the node group preset that is the default in the active graph\. For information about presets, see [Comment and Group Presets](script-canvas-comment-and-group-presets.md)\. | 
| Ctrl\+Shift\+H | Ungroup | Ungroups the currently selected group\. | 
| Ctrl\+Number\_Key | Create bookmark | Creates a bookmark out of the current view and assigns it to the specified number key\. If you choose a number that is already assigned to a bookmark or a bookmark\-enabled group, you are prompted to reassign the existing bookmark\. For more information about bookmarks, see [Adding Bookmarks for Script Canvas](script-canvas-bookmarks.md)\. For information about enabling groups as bookmarks, see [Grouping Nodes](script-canvas-node-groups.md)\. | 
| Number\_Key | Jump to assigned bookmark location | Jumps to the bookmark location associated with the key that is pressed\. | 
| Ctrl\+Plus Sign \(\+\) | Zoom in | Zooms the graph in\. | 
| Ctrl\+Minus Sign \(\-\) | Zoom out | Zooms the graph out\. | 
| Ctrl\+Shift\+Up Arrow | Zoom to selection | Centers the view on the nodes that are currently selected\. | 
| Ctrl\+Shift\+Down Arrow | Show entire graph | Centers the entire graph into the current display\. Zooms out as much as possible to display all nodes\. | 
| Ctrl\+Shift\+Left Arrow | Show start of chain | Centers the view on the nodes that do not have any input connections, and are connected to the selected node through their output connections\. | 
| Ctrl\+Shift\+Right Arrow | Show end of chain | Centers the view on the nodes that do not have any output connections, and are connected to the selected node through their input connections\. | 
| Ctrl\+K, Ctrl\+C | Comment out selected nodes | Comments out the current selection of nodes and turns them gray\. Commented out nodes are not run at runtime, but still exist at edit time\. | 
| Ctrl\+K, Ctrl\+U | Uncomment selected nodes | Uncomments the selected nodes\. | 

## Mouse Shortcuts<a name="script-canvas-shortcuts-mouse-shortcuts"></a>

The following shortcuts use the mouse or keyboard and mouse\.


****  

| **User Action** | **Result** | **Description** | 
| --- | --- | --- | 
| Alt\+Left Click node | Disconnect and delete a single node or group | Disconnects and deletes the node or group clicked\. | 
| Alt\+Left Click connection | Delete a connection | Deletes the connection clicked from the active graph\. | 
| Alt\+Left Click slot | Delete connections |  Deletes any connections to the slot from the active graph\.  Ensure that the connections that you want to delete are highlighted before pressing **Alt\+Left Click**\. Otherwise, you might delete the node instead\.   | 
| Middle Mouse Button \(Scroll Wheel\) Click graph tab | Close graph | Closes the open graph corresponding to the tab clicked\. If the graph has changed and has not been saved, prompts you to save it first\. | 
| Scroll mouse wheel | Zoom the graph | Zooms the graph in or out\. | 