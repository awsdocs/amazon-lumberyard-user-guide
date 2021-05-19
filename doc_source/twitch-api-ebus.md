# Twitch C\+\+ API Reference<a name="twitch-api-ebus"></a>

The Twitch API and its RESTful functions are represented by two EBus's in Lumberyard:
+ **TwitchApiRequestBus**
+ **TwitchApiNotifyBus**

**Note**  
If you are using the legacy Twitch v5 Gem, the EBus's are the **TwitchRequestBus** and the **TwitchNotifyBus**\.

EBus is the interface that's used to make RESTful requests to the Twitch API\. For each function in the [Twitch API Reference](https://dev.twitch.tv/docs/api/reference), there is a corresponding call in the `TwitchApiRequestBus` that will queue an HTTP request\. The Twitch API Gem also includes additional EBus functions, which are detailed in the following sections\.

For general information about using event buses in Lumberyard, see [Working with the Event Bus \(EBus\) system](ebus-intro.md)\.

Each call made on the `TwitchApiRequestBus` leads to a response you can subscribe to and listen to on the `TwitchApiNotifyBus`\. Because calls are made asynchronously, responses are not guaranteed to arrive in the same order as requested\. Each response typically includes the following data:
+ a unique `TwitchApi::ReceiptId`
+ a `TwitchApi::ResultCode`
+ data from the JSON response

To determine which response corresponds to a request, you can compare the `ReceiptId` in your requests to the `ReceiptId` in the responses\.

To determine if the call was successful, check if `result.m_result` is equal to `ResultCode::Success`\.

The requested data can be found in `result.m_value.m_data`\. The TwitchApi Gem handles parsing the JSON responses served by the Twitch API into these data structs\. These structs are also reflected in Lumberyard's BehaviorContext so that they are fully usable from Lua and ScriptCanvas\. Note that the structs are not necessarily identical to the JSON response format returned by Twitch\. They may have been packed down to reduce layers\.

Example handler for **GetExtensionAnalytics**\.

```
void OnGetExtensionAnalytics(const ExtensionAnalyticsResult& result) override
{
    // Check to see if this is the response we're looking for.
    if( result.GetId() == sentRequest.GetID() )
    {
        // Display Extension Analytics info. Note this call can return multiple results.
        cout << "Request Twitch Extension Analytics Info" << endl;
        if(result.m_result == TwitchApi::ResultCode::Success)
        {
            // Iterate through all results
            for (const TwitchApi::ExtensionAnalyticsDatum& datum : result.m_value.m_data)
            {
                cout << " Extension Id   : " << datum.extension_id << endl;
                cout << " Type           : " << datum.type << endl;
                cout << " URL            : " << datum.url << endl;
                cout << " Started-At Time: " << datum.started_at << endl;
                cout << " Ended-At Time  : " << datum.ended_at << endl;
            }
        }
        else
        {
            cout << "Failed Result: " << result.m_result << endl;
        }
    }
}
```

`ExtensionAnalyticsResult` is populated from the JSON response received from the Twitch API\. The JSON response would have been formatted like this:

```
{
   "data": [
      {
         "extension_id": "abcdefg",
         "URL": "https://my.twitch.test/123",
         "type": "overview_v1",
         "date_range": {
            "started_at": "2018-04-30T00:00:00Z",
            "ended_at": "2018-05-01T00:00:00Z"
         }
      }
   ]
}
```

Note that the JSON has `started_at` and `ended_at` contained within the `date_range` object\. The TwitchApi Gem simplifies the response struct for this call by eliminating `date_range` and placing `started_at` and `ended_at` adjacent to the rest of the data\. As a design decision, the TwitchApi Gem tries to keep structs as lean as possible so each response struct may be a leaner version of the JSON response\.

**Topics**
+ [TwitchApiRequestBus](twitch-api-ebus-request-bus.md)
+ [TwitchApiNotifyBus](twitch-api-ebus-notify-bus.md)