# Generating and Setting a Twitch Client ID<a name="chatplay-generate-twitch-client-id"></a>

In order for Twitch ChatPlay and Twitch API features to function properly, you must set the following console variables to use your application's client ID:
+ For Twitch ChatPlay, set `chatPlay_ClientID`
+ For Twitch API, set `broadcast_ClientID`

You can use the same value for both console variables\.

If you have already registered your application with Twitch, you can locate your client ID on the [Twitch Dev site](https://dev.twitch.tv/)\. Click **My Applications** and then select **Manage** on the name of your application\.

## Generate a Client ID<a name="generate-twitch-client-id-howto"></a>

Generate a client ID by following the instructions below\.

**To generate the client ID**

1. Go to the [Twitch Dev site](https://dev.twitch.tv/) and log in to your account\.

1. Under **My Applications**, choose **Register an App**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/chatplay/twitch-client-id-dev-site.png)

1. On the **Dashboard**, under **Developer Applications**, choose **Register Your Application**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/chatplay/twitch-client-id-register-app-dashboard.png)

1. On the **Register Your Application** page, complete the form and choose **Register**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/chatplay/twitch-client-id-register-application-page.png)

1. Note the generated client ID that you will use to set your console variables\.

## Set the Client ID<a name="set-twitch-client-id-howto"></a>

Set the client ID by following the instructions below for your version of Lumberyard\.

**To set the client ID \(Lumberyard 1\.6 or later\)**

1. On your computer, navigate to your project's `game.cfg` file \(located in the `\dev\project_name\` directory at the root of your Lumberyard installation\)\.

1. Edit the `game.cfg` file to add the following:

   ```
   chatPlay_clientID = "client ID generated from Twitch"
   broadcast_clientID = "client ID generated from Twitch"
   ```

**To set the client ID \(Lumberyard 1\.5 or earlier\)**

1. Modify the `HttpRequestManager.cpp` file \(located in the `\dev\Code\CryEngine\CryAction\HttpCaller` directory\) to add the following line in the `HttpRequestManager::HandleRequest` function: `httpRequest->SetHeaderValue("Client-ID","client ID generated from Twitch");`

   It should appear as follows:

   ```
   auto httpRequest = Aws::Http::CreateHttpRequest(uri, httpRequestParameters.GetMethod(), 
   Aws::Utils::Stream::DefaultResponseStreamFactoryMethod);
   httpRequest->SetHeaderValue("Client-ID","client ID generated from Twitch");
   auto httpResponse = httpClient->MakeRequest(*httpRequest);
   ```

1. Rebuild the game and engine\.