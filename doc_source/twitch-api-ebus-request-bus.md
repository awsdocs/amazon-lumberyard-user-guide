# TwitchApiRequestBus<a name="twitch-api-ebus-request-bus"></a>

The `TwitchApiRequestBus` includes functions that correspond to their counterparts defined in the [Twitch API Reference](https://dev.twitch.tv/docs/api/reference), plus the following additional functions\.

## SetApplicationID<a name="twitch-api-ebus-request-setapplicationid"></a>

Sets the Twitch application ID\. This must be called before any other API operation, and should only be called once\. You will not receive a notification from this call\.

**Usage Example**

```
/*
** Set a string to hold our Twitch Application ID.
*/
 
AZStd::string applicationId = "0123456789abcdef0123456789";
 
TwitchApi::TwitchApiRequestBus::Broadcast(&TwitchApiRequests::SetApplicationId, applicationId);
```Parameters

*applicationID \(AZStd::string\)*  
The Twitch application ID that you obtain from Twitch when you create an application\.

**Return**  
No return value\.

## SetAppAccessToken<a name="twitch-api-ebus-request-setappaccesstoken"></a>

Sets the Twitch app access OAuth token\. When you set the app access token, a new `AppAccessTokenNotify` event is generated on the `TwitchApiNotifyBus` EBus and `TwitchApi::TwitchApiNotifications::AppAccessTokenNotify()` is called\.

**Usage Example**

```
/*
** Set a string to hold our Twitch app access OAuth bearer token.
*/

AZStd::string appToken = "0123456789abcdef0123456789";
 
TwitchApi::TwitchApiRequestBus::Broadcast(&TwitchApiRequests::SetAppAccessToken, appToken);
```Parameters

*token \(AZStd::string\)*  
The Twitch app access OAuth bearer token\.

**Return**  
No return value\.AppAccessTokenNotify Callback

*token \(`AZStd::string`\)*  
The Twitch app access OAuth token that was set\.

## SetUserAccessToken<a name="twitch-api-ebus-request-setuseraccesstoken"></a>

Sets the Twitch user access OAuth token\. When you set the user access token, a new `UserAccessTokenNotify` event is generated on the `TwitchApiNotifyBus` EBus and `TwitchApi::TwitchApiNotifications::UserAccessTokenNotify()` is called\.

**Usage Example**

```
/*
** Set a string to hold our Twitch user access OAuth bearer token.
*/

AZStd::string userToken = "0123456789abcdef0123456789";
 
TwitchApi::TwitchApiRequestBus::Broadcast(&TwitchApiRequests::SetUserAccessToken, userToken);
```Parameters

*token \(AZStd::string\)*  
The Twitch user access OAuth bearer token\.

**Return**  
No return value\.UserAccessTokenNotify Callback

*token \(`AZStd::string`\)*  
The Twitch user access OAuth token that was set\.

## SetUserId<a name="twitch-api-ebus-request-setuserid"></a>

Sets the Twitch user ID\. When you set the user ID, a new `UserIdNotify` event is generated on the `TwitchApiNotifyBus` EBus and `TwitchApi::TwitchApiNotifications::UserIdNotify()` is called\.

**Usage Example**

```
/*
** Set a string to hold our Twitch user ID.
*/

AZStd::string userId = "0123456789abcdef0123456789";
 
TwitchApi::TwitchApiRequestBus::Broadcast(&TwitchApiRequests::SetUserId, userId);
```Parameters

*userId \(AZStd::string\)*  
The Twitch User ID\. This can be obtained from Twitch by querying a user name\.

**Return**  
No return value\.UserIdNotify Callback

*userID \(`AZStd::string`\)*  
The user ID that was set\.

## GetApplicationId<a name="twitch-api-ebus-request-getapplicationid"></a>

Gets the cached Twitch application Id\. There is no notification from this call\.

**Usage Example**

```
/*
** Get our Twitch Application ID.
*/

AZStd:string applicationId;
  
TwitchApi::TwitchApiRequestBus::BroadcastResult(applicationId, &TwitchApiRequests::GetApplicationId);
```

**Parameters**  
No parameters\.Return

*applicationId \(AZStd::string\)*  
The Twitch application ID\. This is obtained from Twitch when you create the application\.

## GetAppAccessToken<a name="twitch-api-ebus-request-getappaccesstoken"></a>

Gets the cached Twitch app access OAuth token\. There is no notification from this call\.

**Usage Example**

```
/*
** Get the Twitch app access OAuth bearer token.
*/

AZStd:string oAuthToken;
  
TwitchApi::TwitchApiRequestBus::BroadcastResult(oAuthToken, &TwitchApiRequests::GetAppAccessToken);
```

**Parameters**  
No parameters\.Return

*oAuthToken \(AZStd::string\)*  
The Twitch app access OAuth bearer token\.

## GetUserAccessToken<a name="twitch-api-ebus-request-getuseraccesstoken"></a>

Gets the cached Twitch user access OAuth token\. There is no notification from this call\.

**Usage Example**

```
/*
** Get the Twitch user access OAuth bearer token.
*/

AZStd:string oAuthToken;
  
TwitchApi::TwitchApiRequestBus::BroadcastResult(oAuthToken, &TwitchApiRequests::GetUserAccessToken);
```

**Parameters**  
No parameters\.Return

*oAuthToken \(AZStd::string\)*  
The Twitch user access OAuth bearer token\.

## GetUserId<a name="twitch-api-ebus-request-getuserid"></a>

Gets the cached Twitch user ID\. There is no notification from this call\.

**Usage Example**

```
/*
** Get the Twitch user ID.
*/

AZStd:string userId;
  
TwitchApi::TwitchApiRequestBus::BroadcastResult(userId, &TwitchApiRequests::GetUserId);
```

**Parameters**  
No parameters\.Return

*userId \(AZStd::string\)*  
The Twitch user ID\.