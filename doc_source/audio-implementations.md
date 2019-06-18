# Audio Implementations<a name="audio-implementations"></a>

The Audio Implementation translates generic Audio Translation Layer \(ATL\) state requests into real calls to the middleware API\. Audio Implementation also implements low\-level hooks for file I/O and memory allocation as needed for the audio middleware\.

Lumberyard provides two Audio Implementation modules:

1. `CryAudioImplWwise` – Uses Audiokinetic Wwise\.

1. `CryAudioImplNoSound` – Does not use any audio middleware software and does not produce audio output\. This module is primarily provided as an example\.

**Topics**
+ [AudioKinetic Wwise](audio-wwise.md)