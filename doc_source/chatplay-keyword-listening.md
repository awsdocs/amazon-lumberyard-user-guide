# Listening for Twitch Keywords<a name="chatplay-keyword-listening"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

This topic discusses how to set up the Flow Graph logic required to listen for keywords from the Twitch chat window\.

**To listen for keywords**

1. In the **Flow Graph Editor**, under **Components, **drag the **Game:Start** node onto the graph\.

1. Under **Components**, drag two **Twitch:ChatPlay:Keyword** nodes onto the graph next to the **Game:Start** node\.

1. Connect the **output** of the **Game:start** node to the **Start** inputs of both **Twitch:ChatPlay:Keyword** nodes\.

![\[\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)