# Troubleshooting Twitch ChatPlay<a name="chatplay-debugging"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

If you run into problems while connecting Twitch ChatPlay to your game, review the following troubleshooting tips for a possible solution\.

If your game fails to connect to your Twitch channel, ensure the following:
+ You properly entered the name of your Twitch channel into your flow graph\.
+ You have an active Twitch account set up with the channel name that you're using\.
+ You have activated the **ChatPlay** node in your flow graph\.
+ You have an active Internet connection\.

If your game fails to connect to your Twitch channel after a successful first attempt, make sure that you have successfully disconnected from your Twitch channel using the **DisconnectAll** node in your flow graph\. Failing to do so may result in a successful connection the first time, and then failure to connect afterwards because the first connection was left open\.