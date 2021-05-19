# Engaging Broadcasters and Viewers on Twitch<a name="twitch-intro"></a>

Lumberyard is integrated with Twitch so that you can build games that engage with broadcasters and viewers on Twitch\.

**Twitch ChatPlay**  
The Twitch ChatPlay feature within Lumberyard helps you build gameplay that interacts in real time with Twitch viewers\. For example, you can build a game where viewers can vote on game outcomes, gift power\-ups to their favorite players, or change the level based on the number of viewers watching the player\.

**Twitch JoinIn**  
The Twitch JoinIn feature within Lumberyard helps you build multiplayer games that allow Twitch broadcasters to invite fans to join them side by side in the game\. Once invited, a fan can jump into the broadcaster's game with a single click in the Twitch chat channel, while others continue to watch\.

**Twitch API**  
 Twitch API functionality in Lumberyard is based on the publicly available RESTful functions described in the [Twitch API reference](https://dev.twitch.tv/docs/api/reference)\. Each of these functions has a corresponding call in the Lumberyard **TwitchApiRequestBus** that will queue an HTTP request\. You can listen for the response to this request on the **TwitchApiNotifyBus**\.

## Prerequisites<a name="gems-system-gem-twitch-prerequisites"></a>

To use the Twitch gem and add Twitch support to your Lumberyard project, you must:
+ Be authorized as a Twitch development partner\. To register, visit the Twitch Developer Portal at [https://dev\.twitch\.tv/](https://dev.twitch.tv/)\.

**Topics**
+ [Prerequisites](#gems-system-gem-twitch-prerequisites)
+ [Twitch ChatPlay System](chatplay-intro.md)
+ [Twitch C\+\+ API Reference](twitch-api-ebus.md)