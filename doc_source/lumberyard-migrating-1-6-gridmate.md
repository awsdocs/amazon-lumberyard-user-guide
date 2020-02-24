# Migrating GridMate Service Sessions<a name="lumberyard-migrating-1-6-gridmate"></a>

In Lumberyard 1\.6, the way that GridMate handles session services has been refactored to enable multiple session services to co\-exist\. Previously only a single session service could be active and all requests were made through a generalized interface\. The generalized interface has been removed and now EBuses must be used to communicate with each session service\. The following changes may require you to migrate built\-in services to the new methods or to update any custom services that you have created\.

## RegisterService<a name="lumberyard-migrating-1-6-gridmate-change-1"></a>

`RegisterService` now uses `GridMateServiceId` to associate with the given service\. The ID is used to unregister the service and should be unique to each instance of the service\.

The following changes are required:
+ Any calls to `RegisterService` must now pass along this ID\.
+ Any calls to the templated function `StartGridMateService` will work for the built\-in session services such as `LANSessionService` and `GameliftSessionService`\. 
  + Any custom session services that are registered through the function must now implement the static function `GetGridMateServiceId` inside the class definition\.
  + The macro `GRIDMATE_SERVICE_ID` intakes the service name and creates the appropriate function\. For example, `GRIDMATE_SERVICE_ID(MyCustomSessionService)`\.

## UnregisterService<a name="lumberyard-migrating-1-6-gridmate-change-2"></a>

`UnregisterService` now uses `GridMateServiceId` instead of `GridMateService*`\.

The following changes are required:
+ A new template function called `StopGridMateService` helps to standardize the helpers workflow\. This helper will work for the built\-in session services such as `LANSessionService` and `GameliftSessionService`\.
  + Any custom session services that want to use this method must implement the static function `GetGridMateServiceId` inside the class definition\.
  + The macro `GRIDMATE_SERVICE_ID` intakes the service name and creates the appropriate function\. For example, `GRIDMATE_SERVICE_ID(MyCustomSessionService)`\.

## HostSession, JoinSession, and StartGridSearch<a name="lumberyard-migrating-1-6-gridmate-change-3"></a>

`HostSession`, `JoinSession` \(all varieties\), and `StartGridSearch` have been removed from the `IGridMate` class\.

The following changes are required:
+ The removed methods no longer make sense when deciding which session service to use\. Multiple session services offer the ability to accept different search parameters and implement a different subset of the join requests\.
+ Each built\-in session service now implements an EBus that exposes the specific methods for the session service\. The EBus is identified by the `IGridMate*` instance to which the service is registered\. Any calls to the `IGridMate*` methods must be replaced by service\-specific EBus calls\.

## Host, Connect, and ListServers Nodes<a name="lumberyard-migrating-1-6-gridmate-change-4"></a>

The general purpose flow graph nodes for `Host`, `Connect`, and `ListServers` have been removed because the general purpose interface no longer exists\.

The following changes are required:
+ Flow graph nodes were created for each of the built\-in session services\. These service\-specific nodes must be used in order to create a unified flow\. For an example of how these nodes work in a multi\-platform game, see the MultiplayerLobby level in the Multiplayer Project\.