# Flight<a name="ai-concepts-flight"></a>

Use these archetypes and flow nodes in conjunction with entities to control flying vehicles\. See these archetypes in the characters archetype library: 
+ **CELL/Helicopter\.Regular**
+ **Ceph/Dropship\.Regular**
+ **Ceph/Gunship\.Regular**

The following flow nodes to be used with these entities are found under the Helicopter category\.

## FollowPath<a name="ai-concepts-flight-followpath"></a>

This flow node sets the current path that the flight AI uses\.
+ When the AI is not in combat mode\.
  + If the AI is set to loop through the flow node path, the AI tries to go from its current location to the closest point of the path and then follows it to the end\. The node outputs indicating that the AI has reached the end of the path is sent once only\.
  + Without looping, the AI tries to go from its current location to the beginning of the path and then follows it to the end\.
+ When the AI is in combat mode\. 
  + If the target is visible, the path is used to position the AI in the best location to attack the target\. It is also used to navigate between positions within the path\.
  + If the target is not visible, the path is used as a patrol path\. Where possible, it simplifies setup to have paths in combat mode be set to loop\.

## EnableCombatMode<a name="ai-concepts-flight-enablecombatmode"></a>

This flow node enables or disables the AI's ability to position itself within the combat path in order to engage and shoot at its current target\. By default, an AI is not in combat mode until it's explicitly allowed to go into combat mode\.
+ When an AI is in combat mode and has identified a target location, it will try to reposition itself within the current path to a position from which it can engage\.
+ Any character of an opposing faction is a good candidate for a target\.

## EnableFiring<a name="ai-concepts-flight-enablefiring"></a>

This flow node enables or disables the ability of the AI to shoot at its current target when in combat mode\. By default, an AI is allowed to fire when in combat mode until it's explicitly disabled using this node\.