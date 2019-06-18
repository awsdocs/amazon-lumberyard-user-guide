# Debugging Agent Spawning Issues<a name="ai-spawning-debug"></a>

You can use the following console variables to debug AI entity pool issues:

Unless otherwise noted, variable type is Boolean and default value is 0\.
+ **ai\_StatsDisplayMode 1** \- Useful to check the number of currently active AI agents\.
+ **es\_DebugPool 1** \- Used to debug entity pools\.
+ **es\_DebugPoolFilter ** – Enter the name of the entity pool as the value\.

The following represents different information that is available from debug output:
+ **Bookmarked Entities** \- Number of entities marked as being created through pools\. It should be greater than 0 if you have AI agents in your level that should be marked\.
+ **Pool Name** \- The entity pool whose information is about to follow\. The name should be assigned to the es\_DebugPoolFilter variable to get more information about the pool\. The color highlight on this text means the following:
  + White means the pool has no issues\.
  + Yellow means the pool has reached maximum capacity at some point during the level\. It is a warning \-the pool is still being used correctly, but at the maximum\. 
  + Red means the pool reached its maximum capacity and another entity was trying to be prepared from the pool, but failed\. 
+ **Not In Use** \- The current number of slots in the entity pool that are not in use\.
+ **In Use** \- The current number of slots in the entity pool that are currently being used\. Below this output, the AI that is currently prepared from the pool and exists is shown, followed by their EntityId\.
+ **Pool Definitions** \- The entity classes that exist in the pool\. Max count \(size of the pool\) is displayed on the first line\. The color highlight of the class name displays information about how that class has been used with the pool, as follows:
  + White means no entities have been prepared from the pool yet of that class type\.
  + Green means at least one entity has been prepared and all so far have been prepared successfully\.
  + Red means at least one entity has been prepared but it failed when being prepared\.