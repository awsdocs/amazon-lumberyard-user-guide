# Twitch ChatPlay System<a name="chatplay-intro"></a>

Twitch ChatPlay provides a flexible framework to create customized game interactions between broadcasters and spectators on Twitch, the world’s leading social video platform and community for gamers\.

Twitch ChatPlay includes support for chat commands, polls, and surveys that can be triggered by Twitch viewers through the Twitch chat channel\. For example, you can create a chat command \#cheer that triggers celebration animations in your game\.

Twitch ChatPlay is implemented by a set of flow graph nodes that establish a connection to a Twitch channel and use incoming traffic as a game input, like any other input device\.

For a tutorial on Twitch ChatPlay, see [Amazon Lumberyard Tutorials](http://gamedev.amazon.com/forums/tutorials)\.

Twitch ChatPlay includes the following components and services:
+ Twitch IRC servers
+ Twitch ID authentication
+ Twitch account

In addition, [Twitch JoinIn](chatplay-joinin.md) enables broadcasting players on Twitch to invite targeted viewers into their game sessions on demand\.

The following diagram illustrates Twitch ChatPlay's server\-side components\.

![\[Twitch ChatPlay server-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Twitch ChatPlay server-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Twitch ChatPlay server-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

The following diagram illustrates Twitch ChatPlay's client\-side components\.

![\[Twitch ChatPlay client-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Twitch ChatPlay client-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)![\[Twitch ChatPlay client-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/)

**Topics**
+ [Setting up a Twitch ChatPlay Channel](chatplay-setup-channel.md)
+ [Listening for Twitch Keywords](chatplay-keyword-listening.md)
+ [Using Flow Graph with Twitch ChatPlay](chatplay-flow-nodes.md)
+ [Twitch ChatPlay Console Variables, Classes, and Connection Methods](chatplay-console-variables.md)
+ [Generating and Setting a Twitch Client ID](chatplay-generate-twitch-client-id.md)
+ [Troubleshooting Twitch ChatPlay](chatplay-debugging.md)