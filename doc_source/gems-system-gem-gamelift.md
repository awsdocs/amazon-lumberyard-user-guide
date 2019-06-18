# GameLift Gem<a name="gems-system-gem-gamelift"></a>

Amazon GameLift is an AWS service for deploying, operating, and scaling session\-based multiplayer games\. With Amazon GameLift, you can quickly scale high\-performance game servers up and down to meet player demand without any additional engineering effort or upfront costs\.

The GameLift gem makes it easy for you to use Amazon GameLift in Lumberyard\. To use the Amazon GameLift service, you simply enable the GameLift Gem in your Lumberyard projects\.

The GameLift gem provides two services: On the server side, it provides the `GameLiftServerService`\. On the client side, it provides the `GameLiftClientService`\. When you use the GameLift Gem in your game project, the following sequence of events occurs:
+ The server starts the `GameLiftServerService` and listens for events delivered by the `GameLiftServerService`\.
+ The client starts the `GameLiftClientService`, sends `GameLiftSessionRequest`, searches `GameLiftSession`, joins `GameLiftSession`, and listens for events delivered by the `GameLiftClientService`\.

These events are illustrated in the following diagram\.

![\[GameLift session workflow\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/game-lift-gem-workflow.png)

## Sample Code<a name="gems-system-gem-gamelift-sample-code"></a>

The GameLift code in this section follows the workflow illustrated in the preceding diagram and is separated into server\-side code and client\-side code\. The code is enabled only when `BUILD_GAMELIFT_SERVER` and `BUILD_GAMELIFT_CLIENT` are defined\.

### Server\-side Code<a name="gems-system-gem-gamelift-sample-code-server-side"></a>

Use the following sample code as a guide when starting and hosting a GameLift server session\.

<a name="gems-system-gem-gamelift-sample-code-start-gameliftserverservice.title"></a>Start GameLiftServerService

```
GridMate::GameLiftServerServiceDesc serviceDesc;
serviceDesc.m_port = settings.m_serverPort;
if (settings.m_logPath)
{
    serviceDesc.m_logPaths.push_back(settings.m_logPath);
}

m_service = GridMate::StartGridMateService<GridMate::GameLiftServerService>(m_gridMate, serviceDesc);
```

<a name="gems-system-gem-gamelift-sample-code-host-a-session.title"></a>Host a Session

```
carrierDesc.m_port = s_gameLiftSettings.m_serverPort;
carrierDesc.m_driverIsFullPackets = false;
carrierDesc.m_driverIsCrossPlatform = true;

EBUS_EVENT_ID_RESULT(session, m_gridMate, GridMate::GameLiftServerServiceBus, HostSession, sp, carrierDesc);
```

### Client\-side Code<a name="gems-system-gem-gamelift-sample-code-client-side"></a>

Use the following sample code as a guide when using the GameLift client service\.

<a name="gems-system-gem-gamelift-sample-code-start-gameliftclientservice.title"></a>Start GameLiftClientService

```
GridMate::GameLiftClientServiceDesc serviceDesc;
serviceDesc.m_accessKey = settings.m_accessKey;
serviceDesc.m_secretKey = settings.m_secretKey;
serviceDesc.m_fleetId = settings.m_fleetId;
serviceDesc.m_endpoint = settings.m_endpoint;
serviceDesc.m_region = settings.m_region;

m_service = GridMate::StartGridMateService<GridMate::GameLiftClientService>(m_gridMate, serviceDesc);
```

<a name="gems-system-gem-gamelift-sample-code-send-gameliftsessionrequest.title"></a>Send GameLiftSessionRequest

```
GridMate::GameLiftSessionRequestParams reqParams;
reqParams.m_instanceName = "TestSession";
reqParams.m_numPublicSlots = 16;
reqParams.m_params[0].m_id = "param1";
reqParams.m_params[0].m_value = "value12";
reqParams.m_numParams = 1;
m_sessionRequest = m_service->RequestSession(reqParams);
```

<a name="gems-system-gem-gamelift-sample-code-search-active-sessions.title"></a>Search Active Sessions

```
EBUS_EVENT_ID_RESULT(m_search, m_gridMate, GridMate::GameLiftClientServiceBus, StartSearch, GridMate::GameLiftSearchParams());
```

<a name="gems-system-gem-gamelift-sample-code-join-a-session.title"></a>Join a Session

```
GridMate::CarrierDesc carrierDesc;
carrierDesc.m_port = 33435;
carrierDesc.m_enableDisconnectDetection = true;
carrierDesc.m_connectionTimeoutMS = 10000;
carrierDesc.m_threadUpdateTimeMS = 30;

const GridMate::GameLiftSearchInfo& gameliftSearchInfo = static_cast<const GridMate::GameLiftSearchInfo&>(*gridSearch->GetResult(0));
EBUS_EVENT_ID_RESULT(m_session,m_gridMate,GridMate::GameLiftClientServiceBus,JoinSessionBySearchInfo,gameliftSearchInfo,carrierDesc);
```