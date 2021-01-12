---
layout: page
title: Registering Content
parent: Architectury API
nav_order: 1
---

# Registering Content
{: .no_toc }

---

## Why is registering content so complicated?
Forge **disallows** you to use vanilla `Registry` class for registering content and requires you to register content in the `RegistryEvent.Register<T>` event, this is different than how you register content in fabric or in vanilla.

## Submitting your mod event bus in forge to Architectury API

We will need to pass your mod event bus to Architectury API to allow Architectury API to listen to the registry events on forge. This is impossible without your help, each mod's `ModContainer` handles `EventBus` a little bit easier, and the mod event bus is hidden from other mods.

Now, we will expose our mod event bus to Architectury. In your forge mod constructor, do the following:

**NOTE: The following tutorial only applies to mods using the `javafml` language provider**

```java
EventBuses.registerModEventBus(MOD_ID, FMLJavaModLoadingContext.get().getModEventBus());
```

## Registering our content through Architectury's Registries
**NOTE: The following tutorial is delivered in mojmap**

We will create a lazy registeries object, this variable is lazy because at the point that we statically initialize this class, the mod event bus might not have passed to Architectury API, causing a crash.

```java
public static final Lazy<Registries> REGISTRIES = new Lazy<>(() -> Registries.get(MOD_ID));
```

During your mods' initialization, you may use this `REGISTRIES` field to get the wrapped registries. With that, we can register our items.
```java
Registry<Item> items = REGISTRIES.get().get(net.minecraft.util.registry.Registry.ITEM_KEY);
RegistrySupplier<Item> exampleItem = items.registerSupplied(new Identifier(MOD_ID, "example_item"), () -> new Item(new Item.Settings()));
```

Notice that the value returned is a `RegistrySupplier`, this is because our content may not have been actually registered at this point, we might still be waiting for the registry event.