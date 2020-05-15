# Audio System Overview<a name="audio-architecture"></a>

The Lumberyard audio system consists of modules, components, and content\.

## Modules<a name="audio-architecture-modules"></a>

Lumberyard audio features the following modules:


****  

| Modules | Description | 
| --- | --- | 
| CrySoundSystem |  Contains the audio translation layer \(ATL\) code and manages the state of the audio system in Lumberyard\. Most of this module runs on the audio thread, but it also synchronizes with the main thread\.  | 
| CryAudioImplWwise |  Contains the implementation of `AudioSystemImplementation` interfaces for Wwise\. Contains all Audiokinetic APIs\. This is the only module that links with Wwise libraries\.  | 
| CryAudioImplNoSound |  Contains the implementation of `AudioSystemImplementation` interfaces that don't produce sound output\. This module is an example that you can use as a starting point for implementing a new middleware\.  | 
| EditorAudioControlsEditor |  Lumberyard Editor plugin\. Contains the **Audio Controls Editor** \(ACE\) to create and manage ATL controls\.  | 
| EditorAudioControlsEditorWwise |  Additional module that the **Audio Controls Editor** loads when Lumberyard uses Wwise\.  | 
| EditorNoSound |  Additional module that **Audio Controls Editor** loads when `NoSound` is specified\.  | 

## Components<a name="audio-architecture-components"></a>

The core audio components are included in Lumberyard Editor\. For more information, see [Audio Components](component-components.md#component-entity-audio)\.

## Content<a name="audio-architecture-content"></a>

Lumberyard audio features the following content:


****  

| Content | Description | 
| --- | --- | 
| Media |  Lumberyard loads soundbanks and loose media at runtime\. The audio middleware authoring tools compiles and generates the media files\.  | 
| Project | The audio middleware authoring tools use a project to manage source audio files, adjust sounds and settings, and generate runtime ready media\. The Audio Controls Editor also uses the project to help map ATL controls to the audio middleware equivalents\. | 
| ATL Libraries |  When the audio system maps ATL controls to their audio middleware equivalents, it creates ATL libraries, which are saved as XML files\. Lumberyard loads these libraries at startup and populates the ATL with runtime data so that the game can control the audio system\.  | 