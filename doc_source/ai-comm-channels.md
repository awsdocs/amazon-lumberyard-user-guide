# Using AI Communication Channels<a name="ai-comm-channels"></a>

AI communication channels are used to determine whether an AI agent can communicate at a given time, depending on whether the communication channel is occupied or free\. Communication channels are XML\-based and can be nested and this determines if a parent communication channel is occupied depending on whether a child communication channel is occupied\.

A sample configuration file with multiple communication channels is shown below:

```
    <!--ChannelConfig.xml-->
    <Communications>
            <ChannelConfig>
                <Channel name="Global" minSilence="1.5" flushSilence="0.5" type="global">
                    <Channel name="Group" minSilence="1.5" flushSilence="0.5" type="group">
                        <Channel name="Search" minSilence="6.5" type="group"/>
                        <Channel name="Reaction" priority="2" minSilence="2" flushSilence="0.5" type="group"/>
                        <Channel name="Threat" priority="4" minSilence="0.5" flushSilence="0.5" type="group"/>
                    </Channel>
                    <Channel name="Personal" priority="1" minSilence="2" actorMinSilence="3" type="personal"/>
                </Channel>
            </ChannelConfig>
        </Communications>
```

Where,
+ **minSilence** – Minimum time \(in seconds\) for which the Channel remains occupied after the Communication has completed\.
+ **flushSilence** – Time \(in seconds\) for which a Channel remains occupied after flushing the Channel\. It is used to override the imposed silence time for the Channel which is no longer playing a Communication\. If this attribute is not specified, the value of minSilence is used\.
+ **actorMinSilence** – Minimum imposed time \(in seconds\) to restrict AI actors from playing voice libraries after starting a Communication\.
+ **ignoreActorSilence** – Ignore \(AI\) actor Communication restrictions from the script\.
+ **type** – Personal, group, or global\.
+ **name** – Name of the channel\.
+ **priority** – Priority level\.