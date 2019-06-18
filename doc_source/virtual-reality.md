# Creating Virtual Reality Games in Lumberyard<a name="virtual-reality"></a>

Lumberyard's [virtual reality](ly-glos-chap.md#virtual_reality) system integrates the use of the OculusRift, HTC Vive, and Open Source Virtual Reality \(OSVR\) head\-mounted displays \(HMD\) on PC gaming systems\. Before using these head\-mounted displays, read each manufacturer's safety guide:
+ [Oculus Rift Health and Safety Warning](http://www.oculus.com/warnings)
+ [HTC Vive Safety and Regulatory Guide](http://dl4.htc.com/web_materials/Safety_Guide/Vive/Vive_safety_and_regulatory_guide_ENG-FRC-ESM.pdf)

To activate Lumberyard's virtual reality support, add the appropriate [Virtual Reality Gem\(s\)](virtual-reality-configuring.md) in the Project Configurator and then [build your project](building-your-lumberyard-game-project.md)\. By enabling the appropriate Virtual Reality Gem\(s\), your project becomes capable of working with the supported virtual reality device\(s\), after some additional configuration\. You can also [add new gems](gems-system-gems.md) for other head\-mounted devices\.

Use [console variables \(CVARs\)](virtual-reality-cvars.md) to activate and modify configurable features of the virtual reality system, such as resolution and performance specifications\. 

You can use flow graph modules for the initial game setup and gameplay scripting, for example, to customize such features as the position of the camera, tracking of the attached virtual reality device, current view depending on height of the player, and more\.

For information on Lua scripting functions for VR, see [VR Lua Functions](lua-scripting-ref-vr.md)\.

**Topics**
+ [Configuring your Project for Virtual Reality](virtual-reality-configuring.md)
+ [Configuring Required Console Variables](virtual-reality-cvars.md)
+ [Using the InstantVR Slice](virtual-reality-instant-vr.md)
+ [Setting Up Virtual Reality with Flow Graph](virtual-reality-flowgraph.md)
+ [Previewing your Virtual Reality Project](virtual-reality-preview.md)
+ [Debugging your Virtual Reality Project](virtual-reality-debug.md)
+ [Using EBus Request Bus Interface for Virtual Reality](virtual-reality-ebus.md)
+ [VR Lua Functions](lua-scripting-ref-vr.md)