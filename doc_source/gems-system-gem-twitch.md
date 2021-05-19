# Twitch v5 Gem<a name="gems-system-gem-twitch"></a>

The **Twitch v5** Gem is a wrapper for the Legacy Twitch v5 RESTful API\. Install this Gem into your Lumberyard project to access legacy [Twitch API v5](https://dev.twitch.tv/docs/v5) features\.

**Warning**  
Twitch API v5 is deprecated\. Consider [migrating](https://dev.twitch.tv/docs/api/migration) to the latest version of the Twitch API, which is supported in Lumberyard by the newer [Twitch API Gem](gem-twitch-api.md)\.

For more information on integrating the Twitch v5 Gem with your Lumberyard project, see [Engaging Broadcasters and Viewers on Twitch](twitch-intro.md)\. 

## Enable the Twitch v5 Gem<a name="enable-gem-twitch-v5"></a>

To enable the Twitch v5 Gem, do the following:

1. Use [Project Configurator](configurator-projects.md) to add the **Twitch v5** Gem to your project\. The **Twitch v5** Gem requires the following Gem as a dependency: 
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