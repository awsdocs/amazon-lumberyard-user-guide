# Video Playback<a name="component-videoplayback"></a>


****  

|  | 
| --- |
| Component entity system is in [preview](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#preview) release and is subject to change\.  | 

You can use the **Video Playback** component to play a video file on an object in your Lumberyard level\. For example, you can use a flat or plane object to simulate a movie screen\. You then add the video playback component to it and specify a video file you want to display\. You can use flow graphs or Lua scripting to trigger the video to play, pause, or stop, depending on player actions\.

To use the video playback component, you must perform an initial setup\. This involves installing software \(either FFmpeg or LibAV\), adding the video playback gem to your project, and then rebuilding your project to enable the gem\.

You can also set your video to play in visual stereo \(not audio stereo\)\. To test this feature, you must use a virtual reality head mounted display \(HMD\)\.

Audio is not currently supported with the video playback component\. You can, however, trigger audio playback separately if you want to play audio along with your video\.

## Setting up Video Playback<a name="component-videoplayback-setup"></a>

To set up video playback in Lumberyard, you must install either FFmpeg or LibAV\. 
+ If both LibAV and FFmpeg are installed, Lumberyard uses FFmpeg\.
+ To use LibAV, remove FFmpeg, and follow the instructions for installing LibAV\.

**Note**  
Certain third\-party software may require a license\. Please consult the terms of service before installing the software\.

**To install FFmpeg**

1. Download the DEV and SHARED versions of FFmpeg from [https://ffmpeg\.zeranoe\.com/builds/](https://ffmpeg.zeranoe.com/builds/)\.

1. Open the Lumberyard 3rdParty folder and create a new folder called FFmpeg.

1. Create a folder inside the FFmpeg folder called 3.2 (it must be called exactly "3.2" regardless of the FFmpeg version you are using).

1. Copy the "include" and "lib" folders from the DEV version of FFmpeg to the 3rdParty/FFmpeg/3.2 directory.

1. Copy the "bin" folder from the SHARED version of FFmpeg to the 3rdParty/FFmpeg/3.2 directory.

1. Within the `3.2` directory, you should now have the following:
   + Directory named `bin`
   + Directory named `include`
   + Directory named `lib`

1. Run Lumberyard Setup Assistant and view the **Install optional SDKs** page to verify that Lumberyard detects FFmpeg\.

**To install LibAV**

1. Download LibAV from [http://builds\.libav\.org/windows/](http://builds.libav.org/windows/)\. Select the release\-lgpl build\. As of this writing, version 11\.7 is the latest build\.

1. Open the Lumberyard 3rdParty folder and create a new folder called libav.

1. Create a folder inside the libav folder called 11.7 (it must be called exactly "11.7" regardless of the LibAV version you are using).

1. Extract the `.7z` file to the directory called `11.7`\. To open and extract `.7z` files, you must use a 7z application, such as 7\-Zip\.

   Within the `11.7` directory, you should have the following:
   + Directory named `usr`
   + `config.log`
   + `md5sum`

1. Run Lumberyard Setup Assistant and view the **Install optional SDKs** page to verify that Lumberyard detects LibAV\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-setup.png)

To use the video playback component, you must also install the **Video Playback** gem\. Follow the [Using Gems to Add Modular Features and Assets](gems-system-gems.md) instructions to install the **Video Playback** gem and build your project\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-gem.png)

## Using the Video Playback Component<a name="component-videoplayback-instructions"></a>

The video playback component is available to use in Lumberyard after you have installed the required software, added the **Video Playback** gem to your project, and then rebuilt your project\.

Video playback supports the following container formats:
+ `.mp4`
+ `.mkv` \(recommended\)
+ `.webm` \(recommended\)

Video playback supports the following codecs:
+ `h.264`
+ `h.265`
+ `VP8` \(recommended\)
+ `VP9` \(recommended\)

The basic setup for the video playback component involves placing a camera, adding a static mesh and video playback component, and configuring material\.

**To use the video playback component**

1. If you do not yet have a camera in your scene, place a [camera component](component-camera.md) near where your video playback is to be placed\. 

   You can use the camera to view your video playback\. Ensure that the camera is facing the direction where you place your video playback component\.

1. Create a new component entity by right\-clicking in your scene and clicking **Create new component entity**\.

1. Use the [**Entity Inspector**](component-entity-inspector.md) to add a [static mesh component](component-static-mesh.md) to your new component entity\.

1. Select a **Static asset** for your static mesh component\. This is the object that your video renders onto\. A cube or plane is a good test mesh\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-staticmesh.png)

1. Add the **Video Playback** component to the same entity\. To do this, click **Add Component**, **Rendering**, **Video Playback**\.

1.  In the video playback component's **Video** setting, select the video that you want to display\. 

1. For **Texture name**, enter a name for your texture, preceded by a dollar sign \($\)\. This is a user\-defined field, so it can be anything you want, but it must begin with a $ character to indicate that it is a render target\. For example, **$videotest** is a valid name but **videotest** is not\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-videoname.png)

1. Use the **Frame queue ahead count** setting to set the number of frames to buffer\. Leave this value at **1**, an acceptable value\. A value of **2** or **3** is typically safe as well\.

   Queueing too many frames to buffer \(for example, a value of **100** frames\) can use too much memory and cause performance issues\.

1. Open the [Material Editor](mat-intro.md) \(use the keyboard shortcut **M** to open it quickly\)\.

1. Create a new material by clicking **Add New Item**, as shown in the following picture\. Give the material a descriptive name, such as **myvideomaterial**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-material.png)

1. Under **Texture Maps**, on the **Diffuse** line, enter the name of your video component's **Texture name** field\. Be sure to include the $ character\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-diffuse.png)

1. Close the **Material Editor** and return to the [**Entity Inspector**](component-entity-inspector.md)\. In the static mesh component, for the **Material override** setting, select the material you just created\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-override.png)

 You can trigger the video to play at the start of your game using either flow graphs or Lua scripting\. The following procedure shows you how to create a simple flow graph to start playing the video when your game starts\. 


****  

|  | 
| --- |
| This topic references tools and features that are [legacy](https://docs.aws.amazon.com/lumberyard/latest/userguide/ly-glos-chap.html#legacy)\. If you want to use legacy tools in Lumberyard Editor, disable the [CryEntity Removal gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-cryentity-removal-gem.html) using the [Project Configurator](https://docs.aws.amazon.com/lumberyard/latest/userguide/configurator-intro.html) or the [command line](https://docs.aws.amazon.com/lumberyard/latest/userguide/lmbr-exe.html)\. To learn more about legacy features, see the [Amazon Lumberyard Legacy Reference](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/)\. | 

**To set up a flow graph to start your video**

1.  In the viewport, right\-click on the static mesh/video playback entity\. Then click **Flowgraph**, **Add**\. Type a name for your new flow graph\. 

1.  Drag a **Game:Start** node and a **VideoPlayback:Play** node onto your flow graph\. Connect the **output** port of the **Game:Start** node to the Activate port of the **VideoPlayback:Play** node\. 

    Right\-click **Choose Entity** in the **VideoPlayback:Play** node and click **Assign graph entity**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-flowgraph.png)

1.  To play the game and test your video playback, press **Ctrl G**\. 
**Note**  
Audio playback is not supported with this component\. You can trigger audio playback separately\.

## Setting Up Stereo Video Playback<a name="component-videoplayback-stereo"></a>

Before setting up stereo video playback, ensure that you have completed the setup instructions in [Setting up Video Playback](#component-videoplayback-setup)\.

Stereo video playback means that the video presents a slightly different image for each eye, creating a 3D feel\. *Stereo* in this case refers to visual stereo only; audio is not supported in the video playback component\. While audio is not supported and must be synced externally, it is possible to play back spatialized audio\. To do so, you must use the full, commercial version of Wwise and a 3D spatializer plugin such as Oculus Spatializer or RealSpace 3D\.

To set up stereo video playback, your source video file must be laid out for stereo\. Lumberyard supports videos in a top\-bottom or bottom\-top layout\. You must have a VR headset to verify that the video is playing in stereo\.

To set up stereo video playback, follow the instructions in [Using the Video Playback Component](#component-videoplayback-instructions)\. The only differences in the setup are the following:
+ You must use a source video file with 3D or stereo information
+ Set the **Stereo Layout** property initially to **Auto\-Detect**\. If it fails to auto\-detect, manually set it to **Top\-Bottom** or **Bottom\-Top**\.

  All supported video files should have their stereo layout written into their metadata\. This, however, is not a requirement and may not have been inserted by your encoder\. If you would like to inject stereo metadata into your video, see [https://support\.google\.com/jump/answer/7044297?hl=en](https://support.google.com/jump/answer/7044297?hl=en)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-stereo-layout.png)

When you enter game mode \(using **Ctrl G**\), you should see the left eye of your video play\. If you do not see this, try changing your **Stereo layout** setting\. 

To verify that your video is playing in stereo, you must enter VR mode\. You can enter VR mode by clicking **VR Preview** at the bottom right corner of the viewport\. Then press **Ctrl G** to enter game mode\. If your **VR Preview** button isn’t enabled, or you can’t get into VR preview mode, ensure that your VR headset is working outside of Lumberyard and then restart the Lumberyard editor\. 

Playing stereo video is resource intensive\. Because the video is often close in proximity to the player, it becomes easy to detect inconsistencies and artifacts in the video\. To prevent that, use higher resolution videos whenever possible\. To conserve resources, do not play more than one or two high resolution stereo videos at a time\. 

## Lua Bindings for Video Playback<a name="component-videoplayback-lua"></a>

You can use Lua bindings to interact programmatically with video playback components that you’ve placed in your scene\. Lua provides a way to establish complex logic for playing, pausing, and stopping videos\. 

### Global Functions<a name="component-videoplayback-lua-global"></a>

The following functions provide programming interfaces for the video playback systems\.

#### VideoPlaybackRequestBusSender<a name="VideoPlaybackRequestBusSender"></a>

**Parameters**  
`EntityID`

**Return**  
Returns the `VideoPlaybackRequestBusSender` object that is connected to the specified entity\. For more information, see [VideoPlaybackRequestBusSender Object](#component-videoplayback-videoplaybackrequestbussender)\.

#### VideoPlaybackNotificationBusHandler<a name="VideoPlaybackNotificationBusHandler"></a>

Exposes callbacks to your Lua script that are triggered by events during video playback\.

For more information, see [VideoPlaybackNotificationBusHandler Object](#component-videoplayback-videoplaybacknotificationbushandler)\. 

**Parameters**  
`Table` – The Lua table to which you want to expose the callback functions\. Pass `self` to expose the callbacks to the current Lua script\.  
`EntityId` – 

**Return**  
Returns the `VideoPlaybackRequestBusSender` object that is connected to the specified entity\. For more information, see [VideoPlaybackRequestBusSender Object](#component-videoplayback-videoplaybackrequestbussender)\.

### VideoPlaybackRequestBusSender Object<a name="component-videoplayback-videoplaybackrequestbussender"></a>

The `VideoPlaybackRequestBusSender` object contains functions with which you can send requests to the video playback component\.

`Bool IsPlaying()`  
Returns `true` if the video is playing\. If the video is paused or stopped, returns `false`\.

`Void Play()`  
Plays the video\. If no video is selected or the video is already playing, this has no effect\.

`Void Pause()`  
Pauses the video\. If the video is already paused, this has no effect\. 

`Void Stop()`  
Stops the video and remains on the last frame\. When the video plays again, it begins at the first frame of the video\. If the video is already stopped, this has no effect\. If the video is playing or paused, the video stops\.

`Void EnableLooping(Bool)`  
Sets whether this video automatically restarts from the beginning once the end of the video is reached\. Pass `true` to enable looping or `false` to disable looping\. Looping is disabled by default\.

`Void SetPlaybackSpeed(Float)`  
Sets how fast the video plays\. For example, **1\.0** is normal speed, **0\.5** is half speed, **2\.0** is double speed, and so on\.  
Caution is advised when setting the video speed\. Setting a speed that is too high can result in choppy playback\.

### VideoPlaybackNotificationBusHandler Object<a name="component-videoplayback-videoplaybacknotificationbushandler"></a>

The `VideoPlaybackNotificationBusHandler` object exposes callback functions to your Lua script that are triggered by events that happen during video playback\. 

`Void OnPlaybackStarted()`  
Called when video playback begins\.

`Void OnPlaybackPaused()`  
Called when video playback pauses\. Not called when video stops\. 

`Void OnPlaybackStopped()`  
Called when video playback is stopped by the user\. If the video reaches the end and is not set to loop, this function is not called\. 

`Void OnPlaybackFinished()`  
Called when all frames in the video are played\. This is not called if the user manually stops video playback\. If looping is enabled, this function is called every time the video loops\. 

## Setting Up Video Playback with Flow Graph<a name="component-videoplayback-flowgraph"></a>

Using the [Video Playback flow graph nodes](https://docs.aws.amazon.com/lumberyard/latest/legacyreference/fg-node-ref-videoplayback.html), you can set up video playback actions that trigger based on certain actions\.

In the following flow graph example, the **PlayPauseMovie** input event \(1\) plays or pauses the video on the attached graph entity\. The **StopMovie** input event \(2\) stops the movie\. 

The **PlayPauseMovie** and **StopMovie** events each connect to an **IsPlaying** node \(3\), which checks whether the video should be played, paused, or stopped\.

The **Play** node \(4\) sets **PlaybackSpeed** to **1** \(normal speed\) and enables the **Loop** setting \(Boolean value of **1**\), indicating that video looping is enabled\. The **Play** node \(4\) also triggers the video to play on **Game:Start** \(5\)\.

The **PlaybackEvents** node \(6\) triggers the **Debug** nodes \(7\) to print to the console whenever the video plays, pauses, stops, and finishes\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/component-videoplayback-flow-graph.png)
