# TwitchApiNotifyBus<a name="twitch-api-ebus-notify-bus"></a>

The `TwitchApiNotifyBus` includes handler functions that correspond to the request functions found in the `TwitchApiRequestBus`, including the following callbacks to the request functions defined by the TwitchApi Gem\.

## AppAccessTokenNotify<a name="twitch-api-ebus-notify-appaccesstokennotify"></a>

Notification event for when the Twitch app access OAuth token is set\.

**Usage Example**

```
// Event gets broadcast.
TwitchApiNotifyBus::QueueBroadcast(&TwitchApiNotifyBus::Events::AppAccessTokenNotify, rAppAccessToken);
 
// Event handled in override of TwitchApi::TwitchApiNotifications::AppAccessTokenNotify.
void AppAccessTokenNotify(const AZStd::string& appAccessToken)
{
    // Do something with the app access OAuth token.
}
```Parameters

*token \(AZStd::string\)*  
The Twitch app access OAuth bearer token\.

**Return**  
No return value\.

## UserAccessTokenNotify<a name="twitch-api-ebus-notify-useraccesstokennotify"></a>

Notification event for when the Twitch user access OAuth token is set\.

**Usage Example**

```
// Event gets broadcast.
TwitchApiNotifyBus::QueueBroadcast(&TwitchApiNotifyBus::Events::UserAccessTokenNotify, rUserAccessToken);
 
// Event handled in override of TwitchApi::TwitchApiNotifications::UserAccessTokenNotify.
void UserAccessTokenNotify(const AZStd::string& userAccessToken)
{
    // Do something with the user access OAuth token.
}
```Parameters

*token \(AZStd::string\)*  
The Twitch user access OAuth bearer token\.

**Return**  
No return value\.

## UserIdNotify<a name="twitch-api-ebus-notify-useridnotify"></a>

Notification event for when the Twitch user ID is set\.

**Usage Example**

```
// Event gets broadcast.
TwitchApiNotifyBus::QueueBroadcast(&TwitchApiNotifyBus::Events::UserIdNotify, rUserId);
 
// Event handled in override of TwitchApi::TwitchApiNotifications::UserIdNotify.
void UserIdNotify(const AZStd::string& userId)
{
    // Do something with the user ID.
}
```Parameters

*userId \(AZStd::string\)*  
The Twitch User ID\.

**Return**  
No return value\.