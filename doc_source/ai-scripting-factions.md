# Factions<a name="ai-scripting-factions"></a>

AI agents use factions to determine their behavior when encountering other AI agents\. There are a base set of behaviors such as neutral, friendly and hostile\. For example, when an AI in the "Grunt" faction encounters an AI in the "Players" faction, the encounter will be hostile\. Players encountering "Civilians" will be friendly, etc\.

To set up faction communications: 
+ Create an XML file that defines all the factions in your game and their reactions to each other \(see the example\)\. This file should be placed in `\Games\Scripts\AI\`\. The SDK includes a template faction XML file, called `Factions.xml`\. 
+ Set the Faction property for all of your AI agents to one of the defined factions\. 

Example: Faction setup

```
Factions.xml

<Factions>
    <Faction name="Players">
        <Reaction faction="Grunts" reaction="hostile" />
        <Reaction faction="Civilians" reaction="friendly" />
        <Reaction faction="Assassins" reaction="hostile" />
    </Faction>
    <Faction name="Grunts">
        <Reaction faction="Players" reaction="hostile" />
        <Reaction faction="Civilians" reaction="neutral" />
        <Reaction faction="Assassins" reaction="hostile" />
    </Faction>
    <Faction name="Assassins">
        <Reaction faction="Players" reaction="hostile" />
        <Reaction faction="Civilians" reaction="hostile" />
        <Reaction faction="Grunts" reaction="hostile" />
    </Faction>
    <Faction name="HostileOnlyWithPlayers" default="neutral">
        <Reaction faction="Players" reaction="hostile" />
    </Faction>
    <Faction name="Civilians" default="neutral" />
    <Faction name="WildLife" default="neutral" />
</Factions>
```