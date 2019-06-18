# Using Amazon GameLift<a name="network-gamelift-using"></a>

Lumberyard supports hosting dedicated servers on the cloud by using Amazon GameLift\. Amazon GameLift is a managed AWS service for deploying, operating, and scaling session\-based multiplayer games\. Amazon GameLift is built on AWS’s highly available cloud infrastructure and allows you to quickly scale high\-performance game servers up and down to meet player demand – without any additional engineering effort or upfront costs\. It reduces the time required to build a multiplayer backend from thousands of hours to just minutes\.

To use GameLift in your project, there are two options:
+ Enable the [GameLift Gem](gems-system-gem-gamelift.md) in your project\. Lumberyard has integrated Amazon GameLift, which makes it easier for you to use GameLift\.
+ Enable the Lumberyard [Multiplayer Gem](gems-system-gem-multiplayer.md) in your project \(which requires the GameLift Gem\)\.

For information about configuring GameLift for the multiplayer sample, see [Configuring the Multiplayer Sample for Amazon GameLift](network-multiplayer-gs-gamelift.md)\. For information, see [Using Gems to Add Modular Features and Assets](gems-system-gems.md)\. For more information about GameLift, see [Amazon GameLift](https://aws.amazon.com/gamelift/)\.

## Additional Links<a name="network-gamelift-using-additional-links"></a>
+ [Tutorial: Creating and connecting to a game session \(pdf\)](https://s3.amazonaws.com/gamedev-tutorials/Tutorials/GameLift-Getting_started-(04)_Creating_and_connecting_to_a_game_session.pdf)
+ [Amazon GameLift \- Creating game sessions and connecting \(video\)](https://www.youtube.com/watch?v=zqc9TvLoBE4&feature=youtu.be)
+ [Amazon GameLift Developer Guide](https://docs.aws.amazon.com/gamelift/latest/developerguide/)
+ [Amazon GameLift API Reference](https://docs.aws.amazon.com/gamelift/latest/apireference/)