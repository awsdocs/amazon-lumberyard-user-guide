# Setting up a Lobby<a name="network-lobby-setup"></a>


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

By default, the Lumberyard engine does not provide any specific lobby implementation, but instead provides the code interface required to construct one\. The [Multiplayer Gem](gems-system-gem-multiplayer.md) does, however, provide some useful constructs that aid in lobby creation using [flow graph nodes](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/fg-nodes-managing.html) and a basic lobby implementation using [components](component-components.md), that can be used as is, or as a reference\.

For more information, see the [Multiplayer Gem](gems-system-gem-multiplayer.md)\.