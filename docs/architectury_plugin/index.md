---
layout: page
title: Architectury Plugin
has_children: true
nav_order: 2
---

# Architectury Plugin
{: .no_toc }

---

Architectury Plugin is a Gradle plugin to allow easier multi-modloader set-ups using a common module.

## Things to know
### Same Limitations as Forge Loom
[Read Me](/architectury-documentations/docs/forge_loom) for things to know on using Forge Loom.

### Unstable + Issues
Architectury Plugin is an experimental project, issues may arise, make sure you report them to the issue tracker.

### Gradle Version Support
Architectury Plugin supports **Gradle 5.5.1** and up, with support for Gradle 6.

### Things that are transformed
- `@Environment` and `EnvType` are remapped to `@OnlyIn` and `Dist`
- `@ExpectPlatform` will be transformed to their platform-specific implementations ([Read More](/architectury-documentations/docs/architectury_plugin/platform_specific))
- A fake forge mod will be generated for dev testing to make forge treat the common module as a mod
- Classes annotated with `@ForgeEvent` or `@ForgeEventCancellable` will extend forge's `Event` class on forge.

### Access Transformer / Access Widener
You must have an identical AT and AW for the common module, the fabric module and the forge module, currently, there is no easy way to translate between ATs and AW, you just have to translate them manually, or use mixin `@Invoker` and `@Accessor`.

### Do not use vanilla Registry class for registering
Forge disallows registering to the vanilla `Registry` class, you must defer your registrations to the `RegistryEvent.Add`.

Architectury API provides an abstraction for ForgeRegistries and vanilla's Registry for registering content. ([Read More](/architectury-documentations/docs/architectury_api/registry))
