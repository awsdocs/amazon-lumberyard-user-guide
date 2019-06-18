# ChatPlay Gem<a name="gems-system-gem-chatplay"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

The Twitch ChatPlay Gem provides a flexible framework to create customized game interactions between broadcasters and spectators on Twitch, the world’s leading social video platform and community for gamers\. Twitch ChatPlay includes support for chat commands, polls, and surveys that can be triggered by Twitch viewers through the Twitch chat channel\.

For example, you can create a chat command `#cheer` that triggers celebration animations in your game\. Twitch ChatPlay is implemented by a set of flow graph nodes that establishes a connection to a Twitch channel and uses incoming traffic as game input, like any other input device\.

To use Twitch ChatPlay, you use flow graph nodes to connect to your Twitch channel and to listen for key words and then act on those keywords when they’re sent by a Twitch user\.

## Additional Links<a name="gems-system-gem-chatplay-additional-links"></a>
+ [Tutorial: Adding Twitch ChatPlay ](https://s3.amazonaws.com/gamedev-tutorials/Tutorials/Twitch-Incorporating_Twitch_into_your_game-(01)_Adding_Twitch_ChatPlay.pdf)