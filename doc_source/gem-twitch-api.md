# Twitch API Gem<a name="gem-twitch-api"></a>

The **Twitch API** Gem is a wrapper for the Twitch RESTful API\. Install this Gem into your Lumberyard project to access Twitch features through the [Twitch API](https://dev.twitch.tv/docs/api/reference)\. This Gem makes it simple to engage broadcasters and leverage existing Twitch functionality for your game\.

The Twitch API Gem does not provide a means for fetching information required to authenticate with the Twitch API, such as User ID, Application/Client ID, or Bearer tokens\. You must first provide this information to the Gem through EBus calls\. Information about the types of Bearer tokens and how they can be acquired are detailed in the [Authentication](https://dev.twitch.tv/docs/authentication#types-of-tokens) section of the Twitch developer documentation\.

For more information on integrating the Twitch API Gem with your Lumberyard project, see [Engaging Broadcasters and Viewers on Twitch](twitch-intro.md)\. 

## Enable the Twitch API Gem<a name="enable-gem-twitch-api"></a>

To enable the Twitch API Gem, do the following:

1. Use [Project Configurator](configurator-projects.md) to add the **TwitchApi** Gem to your project\. The **TwitchApi** Gem requires the following Gem as a dependency: 
   + **HttpRequestor** 

1. Configure your project\. Use the following command\.

   ```
   lmbr_waf configure
   ```

1. Build your project\. Use the following command\.

   ```
   lmbr_waf build_win_x64_vs2019_profile -p all --progress
   ```

For more information on Gems, see the [Gems system documentation](gems-system-gems.md)\. 