# Adding Touch \(Collision\) Bending Effects<a name="vegetation-bending-touch-intro"></a>

The touch bending technique simulates a player touching, brushing against, and interacting with vegetation\. Use it for bushes, branches, and bigger leaves with stems\. To implement touch bending, you use UV layout instancing\.

All touch\-bendable vegetation uses a collision proxy to define the volume of bending effect\. By using a collision volume proxy, touch is detected inside the volume\. This volume should be large enough to enclose all branches that are affected by touch bending\. The proxy is physicalized using the **noCollide Physics** setting\.

## Using UV Layout Instancing<a name="vegetation-bending-touch-uv-layout"></a>

UV instancing for touch bending is a type of bone\-and\-rope technique\. By sharing the same UV space, objects can inherit the joint setup from a "master leaf\."

To create UV instances, you duplicate the master leaf of an element or cluster within the same object\. You can rotate, translate, scale, and even change an instance's shape simply by moving individual vertices without changing vertex count\.

To control where branches and leaves should bend, you place joints \(also called helpers or locators\) at various positions on a master leaf, including the tip\. You must follow a specific naming convention for the joints, such as branch1\_1 \(first branch, first joint at the base\)—Branch1\_1 is the base and does not move\.

Make sure the joints snap to the same location as the vertex nodes\. Lumberyard interpolates between these joints using a rope setup, and weights all other joints automatically\. 