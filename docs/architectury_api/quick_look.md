---
layout: page
title: Quick Look
parent: Architectury API
nav_order: 2
---

# Quick Look
{: .no_toc }

---

## Essential Abstractions

| Class Name | Description
| Platform | Provides access to the platform's name, environment, etc.
| Registries | Provides a platform-agnostic wrapper of minecraft registries, should be used to register content. ([Read More](/architectury-documentations/docs/architectury_api/registry))
| KeyBindings | Provides method(s) to register the key bindings.
| CreativeTabs | Provides method(s) to construct creative tabs.
| MenuRegistry | Provides method(s) to construct container menus, and open them.
| RenderTypes | Provides method(s) to register render types for blocks and fluids.
| ReloadListeners | Provides method(s) to register reloading listeners.
| CriteriaTriggersRegistry | Provides method(s) to register criteria triggers.
| ColorHandlers | Provides method(s) to register color handlers.
| BlockEntityRenderers | Provides method(s) to register block entity renderers.
| BiomeModifications | Provides method(s) to modify biome properties.
| PackRepositoryHooks | Provides method(s) to add pack repositories.

---

## Networking Abstractions

| Class Name | Description
| NetworkManager | Provides a Fabric-like networking registry interface.
| NetworkChannel | Provides a Forge SimpleChannel-like networking registry interface.

---

## Hooks

| Class Name | Description
| BiomeHooks | Provides method(s) to access biome properties.
| BlockEntityHooks | Provides method(s) to sync data to the client.
| DyeColorHooks | Provides method(s) to get the color from a DyeColor.
| EntityHooks | Provides method(s) to get the encode ID from an Entity.
| ExplosionHooks | Provides method(s) to get unaccessible values from an Explosion.
| ItemEntityHooks | Provides method(s) to get unaccessible values from an ItemEntity.
| PlayerHooks | Provides method(s) to access unaccessible things from a Player.
| ScreenHooks | Provides method(s) to access unaccessible things from a Screen.

---

## Extensions

| Class Name | Description
| BlockEntityExtensions | Additional extensions to sync data from the server to the client.
| BlockProperties | Additional block properties.

---

## Events

| Class Name | Description
| TooltipEvent | Events related to tooltips. (Client)
| TickEvent | Events related to game ticking.
| TextureStitchEvent | Events related to texture atlas stitching. (Client)
| RecipeUpdateEvent | Event triggered when the client receives recipe updates. (Client)
| PlayerEvent | Events related to players.
| LifecycleEvent | Events related to lifecycle callbacks.
| InteractionEvent | Events related to player interactions.
| GuiEvent | Events related to screens. (Client)
| ExplosionEvent | Events related to explosions.
| EntityEvent | Events related to entities.
| CommandRegistrationEvent | Event triggered when commands should be registered.
| CommandPerformEvent | Event triggered when commands are executed.
| ChatEvent | Events related to chat.
| ClientChatEvent | Events related to chat. (Client)
| ClientLifecycleEvent | Events related to lifecycle callbacks. (Client)
| ClientPlayerEvent | Events related to players. (Client)
| ClientScreenInputEvent | Events related to inputs intercepted by the screen. (Client)
| ClientTickEvent | Events related to game ticking. (Client)
