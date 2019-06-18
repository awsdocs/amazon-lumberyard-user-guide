# Flow Graph Nodes<a name="gems-system-gem-multiplayer-flow-graph-nodes"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

The flow graph nodes in the Multiplayer gem provide networking features to list and connect to servers that are using a particular service or to host a server on that service\. You can use these flow graph nodes to create a simple lobby through which players can search, join, and host an instance of a game\.

## Multiplayer:Functions:LAN:Host<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionslanhost"></a>

Attempts to host a server on the `LANSessionService`\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Attempts to host the server\. | 
| ServerName  | The name of the server\. Returned as part of the result from the LAN:ListServers call\. | 
| MaxPlayers  | The maximum number of players allowed to join the server\. | 
| Map  | The map to load after the session is created on the host\. If empty, the host remains on the current map\. | 
| Port  | The port to use for hosting the game server\. If \-1 is specified, the value of the sv\_port console variable is used\. | 
| DisconnectDetection  | Enables disconnect detection on the server \(that is, whether clients that do not respond within a particular time are dropped from the session\)\. For disconnect detection to be enabled, both the gm\_disconnectDetection console variable \(true by default\) and the DisconnectDetection value must be true\. | 
| ConnectionTimeout  | How long a connection must fail to respond before being disconnected from the session\. To use this setting, you must enable disconnect detection\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | A GridSession was successfully created\. | 
| Failed  | An error occurred during the attempt to create the GridSession\. | 

## Multiplayer:Functions:LAN:ListServers<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionslanlistservers"></a>

Uses the `LANSessionService` to perform a `GridSearch`\. The results can be displayed or used to connect to a particular server\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the flow graph node to perform a GridSearch for active sessions\. | 
| MaxResults  | Specifies the maximum number of results that should be returned from the search\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The search ran successfully\. | 
| Failed  | An error occurred during the search\. | 
| NumResults  | The number of search results that were found\. | 
| Results  | Returns the information about a search result\. This output is returned once for each search result\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Functions:LAN:Connect<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionslanconnect"></a>

Uses the `LANSessionService` to attempt to join the specified server\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the client to attempt to join the selected session\. | 
| Server Address  | The network address of the server\. | 
| Port  | The network port to use\. If \-1 is specified, the value of the cl\_serverport console variable is used\. | 
| Result  | The result generated from LAN:ListServers\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The client successfully joined the chosen session\. | 
| Failed  | An error occurred when the client tried to join the chosen session\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Functions:XBone:Host<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionsxbonehost"></a>

Attempts to host a server on the `XBoneSessionService`\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Attempts to host the server\. | 
| ServerName  | The name of the server\. Returned as part of the result from the XBone:ListServers call\. | 
| MaxPlayers  | The maximum number of players that can join the specified server\. | 
| Map  | The map to load after the session is created on the host\. If empty, the host remains on the current map\. | 
| Port  | The port to use for hosting the game server\. If \-1 is specified, the value of the sv\_port console variable is used\. | 
| DisconnectDetection  | Enables disconnect detection on the server \(that is, whether clients that do not respond within a particular time are dropped from the session\)\. For disconnect detect\-ion to be enabled, both the gm\_disconnectDetection console variable \(true by default\) and the DisconnectDetection value must be true\. | 
| ConnectionTimeout  | How long a connection must fail to respond before being disconnected from the session\. To use this setting, you must enable disconnect detection\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | Activated when a GridSession is successfully created\. | 
| Failed  | Activated when an error is encountered when an attempt is made to create the GridSession\. | 

## Multiplayer:Functions:XBone:ListServers<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionsxbonelistservers"></a>

Uses the `XBoneSessionService` to perform a `GridSearch.` The results can be displayed or used to connect to a particular server\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the flow graph node to perform a GridSearch for active sessions\. | 
| MaxResults  | Specifies the maximum number of results that should be returned from the search\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The search ran successfully\. | 
| Failed  | The search failed to run\. | 
| NumResults  | The number of search results that were found\. | 
| Results  | Returns the information about a search result\. This output is returned once for each search result\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Functions:XBone:Connect<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionsxboneconnect"></a>

Attempts to join the given specified server using the `XBoneSessionService`\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the client to attempt to join the selected session\. | 
| Server Address  | The network address of the server\. | 
| Port  | The network port to use\. If \-1 is specified, the value of the cl\_serverport console variable is used\. | 
| Result  | The result generated from XBone:ListServers\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | Activated when the client successfully joins the chosen session\. | 
| Failed  | Activated when the client encounters an error when attempting to join the chosen session\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Functions:PSN:Host<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionspsnhost"></a>

Attempts to host a server on the `PSNSessionService`


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Attempts to host the sever\. | 
| ServerName  | The name of the server\. Returned as part of the result from the PSN:ListServers call\. | 
| MaxPlayers  | The maximum number of players that can join the server\. | 
| Map  | The map to load after the session is created on the host\. If empty, the host remains on the current map\. | 
| Port  | The port to use for hosting the game server\. If \-1 is specified, the value of the sv\_port console variable is used\. | 
| DisconnectDetection  | Enables disconnect detection on the server \(that is, whether clients that do not respond within a particular time are dropped from the session\)\. For disconnect detection to be enabled, both the gm\_disconnectDetection console variable \(true by default\) and the DisconnectDetection value must be true\. | 
| ConnectionTimeout  | How long a connection must fail to respond before being disconnected from the session\. To use this setting, you must enable disconnect detection\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | Activated when a GridSession is successfully created\. | 
| Failed  | Activated when an error is encountered when an attempt is made to create the GridSession\. | 

## Multiplayer:Functions:PSN:ListServers<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionspsnlistservers"></a>

Uses the `PSNSessionService` to perform a `GridSearch`\. The results can be displayed or used to connect to a particular server\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the flow graph node to perform a GridSearch for active sessions\. | 
| MaxResults  | Specifies the maximum number of results that should be returned from the search\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The search ran successfully\. | 
| Failed  | The search failed to run\. | 
| NumResults  | The number of search results that were found\. | 
| Results  | Returns the information about a search result\. This output is returned once for each search result\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Functions:PSN:Connect<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionspsnconnect"></a>

Uses the `PSNSessionService` to attempts to join the specified server\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Causes the client to attempt to join the selected session\. | 
| Server Address  | The network address of the server\. | 
| Port  | The network port to use\. If \-1 is specified, the value of the cl\_serverport console variable is used\. | 
| Result  | The result generated from PSN:ListServers | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | Activated when the client successfully joins the chosen session\. | 
| Failed  | Activated when the client encounters an error when attempting to join the chosen session\. | 

**Note**  
This node does not provide any options for configuring encryption\. Encryption must be configured before you use this flow graph node\.

## Multiplayer:Gamelift:Start<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayergameliftstart"></a>

Starts the `GameLiftSessionService` using the supplied parameters\. The `GameLiftSessionService` must be started before the GameLift service can be queried or return results\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| AWSAccessKey  | The access key to use with AWS\. | 
| AWSSecretKey  | The secret key to use with AWS\. | 
| AWSRegion  | The region to use with AWS\. | 
| GameLiftEndpoint  | The GameLift endpoint\. This parameter is optional\. | 
| FleetID  | The fleet ID on AWS\. | 
| AliasID  | The alias ID to use on AWS\. Required if no FleetID is supplied\. | 
| PlayerID  | The player ID to use on AWS\. This parameter is optional\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The GameliftSessionService started successfully\. | 
| Failure  | An error occurred when attempting to start the GameLiftSessionService\. | 

## Multiplayer:Gamelift:CreateGameSession<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayergameliftcreategamesession"></a>

Creates a GameLift session using the `GameLiftSessionService`\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate | Creates the session\. | 
| ServerName | The server name of the GameLift server that is instantiated\. The server name is returned in the GameLift:ListServers call\. | 
| Map | The map that the server should be loaded into\. | 
| MaxPlayers | The maximum number of players allowed to join the session\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success | A session was successfully created\. | 
| Failed | An error occurred during the attempt to create a session\. | 
| Results  | The session that was created, if session creation was successful\. | 

## Multiplayer:Gamelift:ListServers<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayergameliftlistservers"></a>

Uses the `GameLiftSessionService` to perform a `GridSearch` and return a list of the `GridSessions` it was able to find\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Activate  | Starts the search\. | 
| MaxResults  | Specifies the maximum number of results that should be returned from the search\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The search ran successfully\. | 
| Failure  | An error occurred during the search\. | 
| NumResults  | The number of search results that were found\. | 
| Results  | The results that were found\. This port activates once per result\. | 

## Multiplayer:Functions:GameLift:Connect<a name="gems-system-gem-multiplayer-flow-graph-nodes-multiplayerfunctionsgameliftconnect"></a>

Attempts to connect to the specified GameLift session\.


**Inputs**  

| Port | Description | 
| --- | --- | 
| Server Address  | The network address of the server\. | 
| Port  | The network port to use\. If \-1 is specified, the value of the cl\_serverport console variable is used\. | 
| Result  | The result generated from GameLift:ListServers\. | 


**Outputs**  

| Port | Description | 
| --- | --- | 
| Success  | The client successfully joined the chosen session\. | 
| Failed  | An error occurred when the client tried to join the chosen session\. | 

**Note**  
If the GameLift service has not started, the flow graph node attempts to start it by using the configuration values specified in the following GameLift CVars\.  
`gamelift_aws_region`
`gamelift_aws_access_key`
`gamelift_aws_secret_key`
`gamelift_fleet_id`

## Examples<a name="gems-system-gem-multiplayer-flow-graph-nodes-examples"></a>

The following example shows how to use flow graph nodes to create and join PSN and LAN sessions\.

![\[PSN and LAN sessions\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems-system-gem-multiplayer-flow-graph-nodes-examples-psn-lan.png)

The following example shows how to use flow graph nodes to create and join a session using GameLift\.

![\[Create and join a GameLift session\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/gems-system-gem-multiplayer-flow-graph-nodes-examples-gamelift.png)