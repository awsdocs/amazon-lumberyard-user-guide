# AI Tactical Point System<a name="ai-tactical-point-system"></a>

The Tactical Point System \(TPS\) provides the AI system with a powerful method of querying an AI agent's environment for places of interest\. It includes the GetHidespot functionality and expands on the "hide" goalop\.

TPS is a structured query language over sets of points in the AI's world\. Using TPS, AI agents can ask intelligent questions about their environment and find relevant types of points, including hidespots, attack points, and navigation waypoints\. The TPS language is simple, powerful, and designed to be very readable\. 

For example, this query requests all points that match the following criteria: 
+ Generate locations within 7 meters of my current location where I can hide from my attention target\.
+ Only accept places with excellent cover that I can get to before my attention target can\.
+ Prefer locations that are closest to me\.

```
hidespots_from_attentionTarget_around_puppet = 7
coverSuperior = true, canReachBefore_the_attentionTarget = true
distance_from_puppet = -1
```

TPS uses a highly efficient method to rank points, keeping expensive operations like raycasts and pathfinding to an absolute minimum\. Queries are optimized automatically\.

**Topics**
+ [Tactical Point System Overview](ai-tactical-point-overview.md)
+ [TPS Query Execution Flow](ai-tactical-point-execution-flow.md)
+ [TPS Querying with C\+\+](ai-tactical-point-cpp-interface.md)
+ [TPS Querying with Lua](ai-tactical-point-lua-interface.md)
+ [TPS Query Language Reference](ai-tactical-point-query-language.md)
+ [Point Generation and Evaluation](ai-tactical-point-generation-evaluation.md)
+ [Integration with the Modular Behavior Tree System](ai-tactical-point-mbt.md)
+ [Future Plans and Possibilities](ai-tactical-point-future.md)