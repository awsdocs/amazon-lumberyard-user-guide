# Configuring the Multiplayer Sample for Amazon GameLift<a name="network-multiplayer-gs-gamelift"></a>

To prepare the multiplayer sample for use with Amazon GameLift, follow the required procedures for server\-side and client\-side configuration\.

## Server\-Side Configuration<a name="network-multiplayer-gs-gamelift-server-side-configuration"></a>

On the server side, overwrite the `GridMate::OnSessionStarted()` handler\. In the handler, synchronize the session state and load the corresponding map if the CVAR `sv_map` is set in the `Multiplayer::Utils::SynchronizeSessionState()` function\.

The following example shows code for server\-side configuration\.

```
void GameManager::OnSessionCreated(GridMate::GridSession* session)
{
     m_gameSession = session;
     if (m_gameSession)
     {          
          if (m_gameSession->IsHost())
          {
               if (gEnv->IsDedicated())
               {
                    Multiplayer::Utils::SynchronizeSessionState(m_gameSession);
               }
          }
     }
}
```

## Client\-Side Configuration<a name="network-multiplayer-gs-gamelift-client-side-configuration"></a>

On the client side, you must configure the following CVARs:

`sv_port`

`sv_map`

`gamelift_aws_access_key`

`gamelift_aws_secret_key`

`gamelift_fleet_id` or `gamelift_alias_id`

`gamelift_end_point`

`gamelift_playerid`

You can set these CVARs with a console command or with the multiplayer sample user interface\.

To use CVARs to set the client side configuration, enter the following console command\.

```
+sv_port 33435 +gamelift_fleet_id <fleet> +gamelift_aws_access_key <aws access key> +gamelift_aws_secret_key <aws secret key>
```

**To use the multiplayer sample user interface to configure Amazon GameLift**

1. By default, the multiplayer sample loads the **Game Lobby** map\. To add or modify the CVARs, click **Amazon GameLift**\.  
![\[Click Amazon GameLift\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/network-multiplayer-gs-gamelift-choose-gamelift.png)

1. Click **Connect**\.  
![\[Click Connect\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/network-multiplayer-gs-gamelift-connect.png)

1. Specify the **Server Name** and the **Map** \(`sv_map`\) to load\.  
![\[Specify server name and map\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/network-multiplayer-gs-gamelift-server-and-map.png)

1. To join automatically, click **Create Server**\. To search active sessions and select a session to join, click **Refresh**, and then click **Join**\.  
![\[Join a session\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/network-multiplayer-gs-gamelift-join-session.png)

## Create an Amazon GameLift Package<a name="network-multiplayer-gs-gamelift-create-gamelift-package"></a>

To create a Amazon GameLift package, complete the following steps\.

**To create a Amazon GameLift package**

1. Before you create an Amazon GameLift package, do the following:
   + Compile game assets
   + Build the Lumberyard executable

1. Run the following commands to create the Amazon GameLift package:

   ```
   mkdir GameLiftPackageWindows
   ```

   ```
   cp -r MultiplayerSample_pc_Paks_Dedicated/* GameLiftPackageWindows/
   ```

   ```
   cp -r Bin64vc140.Dedicated/* GameLiftPackageWindows/
   ```

1. Upload your build and create a fleet from the Amazon GameLift console\. For more information, see [Uploading Your Game to Amazon GameLift](https://docs.aws.amazon.com/gamelift/latest/developerguide//gamelift-build-intro.html)\.

## Secured Connection \(Not Amazon GameLift Specific\)<a name="network-multiplayer-gs-gamelift-secured-connection-non-gamelift"></a>

Amazon GameLift uses the OpenSSL\-based secure socket driver to create a secured connection\. However, instead of verifying the server, the secure socket driver can verify the client\.

To enable a secured connection, make the following change to the `game.cfg` file:

```
gm_netsec_enable = 1
```

If client verification is needed, make the following change to the `game.cfg` file:

```
gm_netsec_verify_client = 1
```

**Note**  
By default, the certificate and private key are loaded from the `multiplayersample.cert.pem` file \(shared by the certificate and CA root\) and from the `multiplayersample.key.pem` file\. To specific different files, use the `gm_netsec_certificate` and `gm_netsec_private_key` CVARs\.