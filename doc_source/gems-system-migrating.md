# Migrating Your Gems<a name="gems-system-migrating"></a>

Beginning in Lumberyard version 1\.5, gems with code should be built as [Using AZ Modules to Initialize Gems](az-modules-intro.md)\. Gems built as AZ modules are better integrated with the Lumberyard's new [component entity system](component-intro.md)\. As of Lumberyard 1\.5, all gems that ship with Lumberyard have been migrated to be AZ modules\.

Legacy gems built with Lumberyard 1\.4 or earlier are still supported, but to avoid issues, we strongly recommend that you migrate them\. If your custom gems make use of the component entity system, you should migrate your gems immediately\.

To migrate a gem, you modify the initialization code and change the gem's public API to use [Working with the Event Bus \(EBus\) System](ebus-intro.md)\. To accomplish this, you must:
+ A\. Rename your gem files
+ B\. Modify your gem code
+ C\. Edit your `gem.json` file
+ D\. Migrate your config files

Perform these procedures for each of your Lumberyard pre\-1\.5 custom gems\.

## A\. Renaming Your Gem\.h File<a name="gems-system-migrating-rename"></a>

In this step, you rename your `IGem.h` file\.

**To rename your gem\.h file**

1. Rename `Include\<GemName>\I<GemName>Gem.h` to `Include\<GemName>\<GemName>Bus.h`

   \(Remove the `I` character and `Gem`, and add `Bus`\)\.

1. Update your `<GemName>.waf_files` to account for the file that you renamed in the first step\.

## B\. Modifying Your Gem Code<a name="gems-system-migrating-modify-code"></a>

**To edit your gem code**

1. Update the include statements that refer to the file that you renamed in the first procedure\.

1. Make the following changes to `<GemName>Bus.h`\.

   1.  Change the class name from `I<GemName>Gem` to `<GemName>Bus`\.

   1. Change the base class from `IGem` to `AZ::EBusTraits`\.

   1. Remove the `CRYINTERFACE_DECLARE` macro\.

   1. Add the following to the top of the class to make it a single handler bus:

      ```
      public:
      ////////////////////////////////////////////////////////////////////////////
      // EBusTraits
      static const AZ::EBusHandlerPolicy HandlerPolicy =  AZ::EBusHandlerPolicy::Single;
      static const AZ::EBusAddressPolicy AddressPolicy =  AZ::EBusAddressPolicy::Single;
      ////////////////////////////////////////////////////////////////////////////
      ```

   1. Add the following after the class definition:

      ```
      using <GemName>RequestBus =  AZ::EBus<<GemName>Requests>;
      ```

      An example of all of these changes is `ILightningArcGem.h` \(now `LightningArcBus.h`\), which before looked like this:

      ```
      // ILightningArcGem.h
      #pragma once
      #include "IGem.h"
       
      class CLightningGameEffect;
      class CScriptBind_LightningArc;
       
      class ILightningArcGem
          : public IGem
      {
      public:
          CRYINTERFACE_DECLARE(ILightningArcGem, 0xf1b3a17f9c61410a, 0x8783fc1ff9854125);
      public:
          virtual CScriptBind_LightningArc* GetScriptBind() const = 0;
          virtual CLightningGameEffect* GetGameEffect() const = 0;
      };
      ```

      And after looks like:

      ```
      // LightningArcBus.h
      #pragma once
      #include <AzCore/EBus/EBus.h>
       
      class CLightningGameEffect;
      class CScriptBind_LightningArc;
       
      class LightningArcRequests
          : public AZ::EBusTraits
      {
      public:
          //////////////////////////////////////////////////////////////////////////
          // EBusTraits overrides
          static const AZ::EBusHandlerPolicy HandlerPolicy = AZ::EBusHandlerPolicy::Single;
          static const AZ::EBusAddressPolicy AddressPolicy = AZ::EBusAddressPolicy::Single;
          //////////////////////////////////////////////////////////////////////////
       
          virtual CScriptBind_LightningArc* GetScriptBind() const = 0;
          virtual CLightningGameEffect* GetGameEffect() const = 0;
      };
      using LightningArcRequestBus = AZ::EBus<LightningArcRequests>;
      ```

1. Convert all calls through the **GemManager** to your code with calls to `EBUS_EVENT(<GemName>RequestBus`, etc\.\)\. For more information, see [Working with the Event Bus \(EBus\) System](ebus-intro.md)\. Here is an example:

   ```
   // BEFORE: calling through the GemManager
   CLightningGameEffect* gameEffect = GetISystem()>GetGemManager()>GetGem<ILightningArcGem>()->GetGameEffect();
   
   // AFTER: calling through the EBus
   CLightningGameEffect* gameEffect = nullptr;
   EBUS_EVENT_RESULT(gameEffect, LightningArcRequestBus, GetGameEffect);
   ```

1. Make the following modifications to the `<GemName>Gem.h` file\.

   1. Change the `<GemName>Gem` base class from `I<GemName>Gem` to `CryHooksModule`

   1. In the `<GemName>Gem` class, add inheritance from `<GemName>RequestBus::Handler`\.
**Note**  
Other classes can implement the bus handler instead\. For example, the OpenVR Gem creates a system component to handle bus requests\. 

   1. Replace the `GEM_IMPLEMENT_WITH_INTERFACE` line with one declaring type information\. This requires the class name, a unique UUID \(Visual Studio has a [tool](https://msdn.microsoft.com/en-us/library/ms241442%28v=vs.80%29.aspx) you can use to get unique values\), and the module base class\. For example:

      ```
      AZ_RTTI(LightningArcGem, "{89724952-ADBF-478A-AFFE-784BD0952E2D}", CryHooksModule);
      ```

   1. Declare a default constructor and destructor\. These used to be declared by the `GEM_IMPLEMENT_WITH_INTERFACE` macro\.

      The following example, from `LightningArcGem.h` shows what the file looked like before the changes:

      ```
      // LightningArcGem.h
      #ifndef _GEM_LIGHTNINGARC_H_
      #define _GEM_LIGHTNINGARC_H_
      #include <GameEffectSystem/IGameEffectSystem.h>
      #include "LightningArc/ILightningArcGem.h"
       
      class LightningArcGem
          : public ILightningArcGem
          , public GameEffectSystemNotificationBus::Handler
      {
      public:
          GEM_IMPLEMENT_WITH_INTERFACE(LightningArcGem, ILightningArcGem, 0x8eccf081ff02476f, 0xb8ec7c4c20cc603c)
          void OnSystemEvent(ESystemEvent event, UINT_PTR wparam, UINT_PTR lparam) override;
          void PostSystemInit();
          void Shutdown();
      public:
          CScriptBind_LightningArc* GetScriptBind() const override;
          CLightningGameEffect* GetGameEffect() const override;
      protected:
          CLightningGameEffect* m_gameEffect;
          CScriptBind_LightningArc* m_lightningArcScriptBind;
          int g_gameFXLightningProfile;
          //////////////////////////////////////////////////////////////////////////
          // GameEffectSystemNotificationBus
          void OnReleaseGameEffects() override;
          //////////////////////////////////////////////////////////////////////////
      };
      #endif //_GEM_LIGHTNINGARC_H_
      ```

      Here is the `LightningArcGem.h` file after the changes are made:

      ```
      // LightningArcGem.h
      #ifndef _GEM_LIGHTNINGARC_H_
      #define _GEM_LIGHTNINGARC_H_
      #include <GameEffectSystem/IGameEffectSystem.h>
      #include <LightningArc/LightningArcBus.h>
       
      class LightningArcGem
          : public CryHooksModule
          , public LightningArcRequestBus::Handler
          , public GameEffectSystemNotificationBus::Handler
      {
      public:
          AZ_RTTI(LightningArcGem, "{89724952-ADBF-478A-AFFE-784BD0952E2D}", CryHooksModule);
          LightningArcGem();
          ~LightningArcGem() override;
          void OnSystemEvent(ESystemEvent event, UINT_PTR wparam, UINT_PTR lparam) override;
          void PostSystemInit();
          void Shutdown();
      public:
          CScriptBind_LightningArc* GetScriptBind() const override;
          CLightningGameEffect* GetGameEffect() const override;
      protected:
          CLightningGameEffect* m_gameEffect = nullptr;
          CScriptBind_LightningArc* m_lightningArcScriptBind = nullptr;
          int g_gameFXLightningProfile;
          //////////////////////////////////////////////////////////////////////////
          // GameEffectSystemNotificationBus
          void OnReleaseGameEffects() override;
          //////////////////////////////////////////////////////////////////////////
      };
      #endif //_GEM_LIGHTNINGARC_H_
      ```

1. Perform the following steps to modify your `<GemName>Gem.cpp` file\.

   1.  If your gem contains `AZ::Component` instances, register them in the constructor: 

      ```
      <GemName>Gem::<GemName>Gem()
      {
          m_descriptors.insert(m_descriptors.back(), {
              <MyComponent>::CreateDescriptor(),
          };
          ...}
      ```

   1. If this class inherits from `<GemName>RequestBus::Handler`, connect to the bus in the constructor and disconnect in the destructor: 

      ```
      <GemName>Gem::<GemName>Gem()
      {
          ...
          <GemName>RequestBus::Handler::BusConnect();
      }
       
       
      <GemName>Gem::~<GemName>Gem()
      {
          <GemName>RequestBus::Handler::BusDisconnect();
          ...
      }
      ```

   1. If there is a call to `RegisterFlowNodes()`, replace it with `RegisterExternalFlowNodes()`\.

   1. Perform the following steps to convert the `REGISTER_GEM` macro to `AZ_DECLARE_MODULE_CLASS`:

      1. Copy the all lower\-case UUID from your `gem.json` file\.

      1. Replace `GEM_REGISTER(<GemName>Gem)` with:

         ```
         AZ_DECLARE_MODULE_CLASS(<GemName>_<GemUUID>, fully qualified module class, usually <GemName>::<GemName>Gem)
         ```

   The following example, `LightningArcGem.cpp`, shows what the file looked like before the changes:

   ```
   // LightningArcGem.cpp
   #include "StdAfx.h"
   #include <platform_impl.h>
   #include <IEntityClass.h>
   #include "LightningArcGem.h"
   #include <FlowSystem/Nodes/FlowBaseNode.h>
   #include "LightningArc.h"
   #include "LightningGameEffect.h"
   #include "ScriptBind_LightningArc.h"
    
   LightningArcGem::LightningArcGem() {}
    
   LightningArcGem::~LightningArcGem() {}
    
   void LightningArcGem::PostSystemInit()
   {
       REGISTER_CVAR(g_gameFXLightningProfile, 0, 0, "Toggles game effects system lightning arc profiling");
       // Init GameEffect
       m_gameEffect = new CLightningGameEffect();
       m_gameEffect->Initialize();
       // Init ScriptBind
       m_lightningArcScriptBind = new CScriptBind_LightningArc(GetISystem());
       // Init GameObjectExtension
       // Originally registered with REGISTER_GAME_OBJECT(pFramework, LightningArc, "Scripts/Entities/Environment/LightningArc.lua");
       // If more objects need registered, consider bringing the macro back along with the GameFactory wrapper.
       IEntityClassRegistry::SEntityClassDesc clsDesc;
       clsDesc.sName = "LightningArc";
       clsDesc.sScriptFile = "Scripts/Entities/Environment/LightningArc.lua";
       static CLightningArcCreator _creator;
       GetISystem()->GetIGame()->GetIGameFramework()->GetIGameObjectSystem()->RegisterExtension("LightningArc", &_creator, &clsDesc);
   }
    
   void LightningArcGem::Shutdown()
   {
       SAFE_DELETE(m_gameEffect);
       SAFE_DELETE(m_lightningArcScriptBind);
   }
    
   void LightningArcGem::OnSystemEvent(ESystemEvent event, UINT_PTR wparam, UINT_PTR lparam)
   {
       switch (event)
       {
       case ESYSTEM_EVENT_GAME_POST_INIT:
           IComponentFactoryRegistry::RegisterAllComponentFactoryNodes(*gEnv->pEntitySystem->GetComponentFactoryRegistry());
           GameEffectSystemNotificationBus::Handler::BusConnect();
           break;
       case ESYSTEM_EVENT_FLOW_SYSTEM_REGISTER_EXTERNAL_NODES:
           RegisterFlowNodes();
           break;
       // Called on ESYSTEM_EVENT_GAME_POST_INIT_DONE instead of ESYSTEM_EVENT_GAME_POST_INIT because the GameEffectSystem Gem
       // uses ESYSTEM_EVENT_GAME_POST_INIT to initialize, and this requires that has happened already.
       case ESYSTEM_EVENT_GAME_POST_INIT_DONE:
           PostSystemInit();
           break;
       case ESYSTEM_EVENT_FULL_SHUTDOWN:
       case ESYSTEM_EVENT_FAST_SHUTDOWN:
           GameEffectSystemNotificationBus::Handler::BusDisconnect();
           Shutdown();
           break;
       }
   }
    
   CScriptBind_LightningArc* LightningArcGem::GetScriptBind() const
   {
       return m_lightningArcScriptBind;
   }
    
   CLightningGameEffect* LightningArcGem::GetGameEffect() const
   {
       return m_gameEffect;
   }
    
   void LightningArcGem::OnReleaseGameEffects()
   {
       Shutdown();
   }
    
   GEM_REGISTER(LightningArcGem)
   ```

   After the changes, `LightningArcGem.cpp` looks like this:

   ```
   // LightningArcGem.cpp
   #include "StdAfx.h"
   #include <platform_impl.h>
   #include <IEntityClass.h>
   #include "LightningArcGem.h"
   #include <FlowSystem/Nodes/FlowBaseNode.h>
   #include "LightningArc.h"
   #include "LightningGameEffect.h"
   #include "ScriptBind_LightningArc.h"
    
   LightningArcGem::LightningArcGem()
   {
       LightningArcRequestBus::Handler::BusConnect();
   }
    
   LightningArcGem::~LightningArcGem()
   {
       LightningArcRequestBus::Handler::BusDisconnect();
   }
    
   void LightningArcGem::PostSystemInit()
   {
       REGISTER_CVAR(g_gameFXLightningProfile, 0, 0, "Toggles game effects system lightning arc profiling");
       // Init GameEffect
       m_gameEffect = new CLightningGameEffect();
       m_gameEffect->Initialize();
       // Init ScriptBind
       m_lightningArcScriptBind = new CScriptBind_LightningArc(GetISystem());
       // Init GameObjectExtension
       // Originally registered with REGISTER_GAME_OBJECT(pFramework, LightningArc, "Scripts/Entities/Environment/LightningArc.lua");
       // If more objects need registered, consider bringing the macro back along with the GameFactory wrapper.
       IEntityClassRegistry::SEntityClassDesc clsDesc;
       clsDesc.sName = "LightningArc";
       clsDesc.sScriptFile = "Scripts/Entities/Environment/LightningArc.lua";
       static CLightningArcCreator _creator;
       GetISystem()->GetIGame()->GetIGameFramework()->GetIGameObjectSystem()->RegisterExtension("LightningArc", &_creator, &clsDesc);
   }
    
   void LightningArcGem::Shutdown()
   {
       SAFE_DELETE(m_gameEffect);
       SAFE_DELETE(m_lightningArcScriptBind);
   }
    
   void LightningArcGem::OnSystemEvent(ESystemEvent event, UINT_PTR wparam, UINT_PTR lparam)
   {
       switch (event)
       {
       case ESYSTEM_EVENT_GAME_POST_INIT:
           IComponentFactoryRegistry::RegisterAllComponentFactoryNodes(*gEnv->pEntitySystem->GetComponentFactoryRegistry());
           GameEffectSystemNotificationBus::Handler::BusConnect();
           break;
       case ESYSTEM_EVENT_FLOW_SYSTEM_REGISTER_EXTERNAL_NODES:
           RegisterExternalFlowNodes();
           break;
       // Called on ESYSTEM_EVENT_GAME_POST_INIT_DONE instead of ESYSTEM_EVENT_GAME_POST_INIT because the GameEffectSystem Gem
       // uses ESYSTEM_EVENT_GAME_POST_INIT to initialize, and this requires that has happened already.
       case ESYSTEM_EVENT_GAME_POST_INIT_DONE:
           PostSystemInit();
           break;
       case ESYSTEM_EVENT_FULL_SHUTDOWN:
       case ESYSTEM_EVENT_FAST_SHUTDOWN:
           GameEffectSystemNotificationBus::Handler::BusDisconnect();
           Shutdown();
           break;
       }
   }
    
   CScriptBind_LightningArc* LightningArcGem::GetScriptBind() const
   {
       return m_lightningArcScriptBind;
   }
    
   CLightningGameEffect* LightningArcGem::GetGameEffect() const
   {
       return m_gameEffect;
   }
    
   void LightningArcGem::OnReleaseGameEffects()
   {
       Shutdown();
   }
    
   AZ_DECLARE_MODULE_CLASS(LightningArc_4c28210b23544635aa15be668dbff15d, LightningArcGem)
   ```

## C\. Editing Your Gem\.json File<a name="gems-system-migrating-edit-gem-json"></a>

A simple change in your `gem.json` file signals Lumberyard that your gem is now an AZ module\.

**To edit the `gem.json` file**

1. Open `gem.json`\.

1. Increment `GemFormatVersion` to `3`\.

## D\. Migrating Your Configuration Files<a name="gems-system-migrating-config-files"></a>

The final step is to update your game's configuration files so that it recognizes your gem as a proper AZ module\.

**To migrate your config files**

1. Open a command prompt and use the `cd` command to navigate to the `Bin64` directory\.

1. Enter the following command:

   ```
   lmbr.exe projects populate-appdescriptors
   ```