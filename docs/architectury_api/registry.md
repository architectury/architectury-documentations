---
layout: page
title: Registering Content
parent: Architectury API
nav_order: 3
---

# Registering Content
{: .no_toc }

---

## Why is registering content so complicated?
Forge **disallows** you to use vanilla `Registry` class for registering content and requires you to register content in the `RegistryEvent.Register<T>` event, this is different than how you register content in fabric or vanilla.

## Submitting your mod event bus in Forge to Architectury API

We will need to pass your mod event bus to Architectury API to allow Architectury API to listen to the registry events on Forge. Each mod's `ModContainer` handles `EventBus` slightly differently, and the mod event bus is inaccessible from other mods.

Now, we will expose our mod event bus to Architectury. In your forge mod constructor, do the following:

**NOTE: The following tutorial only applies to mods using the `javafml` language provider**

```java
EventBuses.registerModEventBus(MOD_ID, FMLJavaModLoadingContext.get().getModEventBus());
```

## Registering our content through Architectury's Registries

### Via Registry
**NOTE: The following tutorial is delivered in mojmap**

We will create a lazy registries object, this variable is lazy because, at the point that we statically initialize this class, the mod event bus might not have passed to Architectury API, causing a crash.

```java
public static final LazyLoadedValue<Registries> REGISTRIES = new LazyLoadedValue<>(() -> Registries.get(MOD_ID));
```

During your mods' initialization, you may use this `REGISTRIES` field to get the wrapped registries. With that, we can register our items.
```java
Registry<Item> items = REGISTRIES.get().get(net.minecraft.core.Registry.ITEM_KEY);
RegistrySupplier<Item> exampleItem = items.registerSupplied(new ResourceLocation(MOD_ID, "example_item"), () -> new Item(new Item.Properties()));
```

Notice that the value returned is a `RegistrySupplier`, this is because our content may not have been registered at this point, we might still be waiting for the registry event.

### Via DeferredRegister

We will create a deferred register, we will then use this to register our entries.

```java
public static final DeferredRegister<Item> ITEMS = DeferredRegister.create(MOD_ID, Registry.ITEM_REGISTRY);
```

After statically defining our deferred register, we can add entries to it, please note that the entries are not registered at this point, so we must refrain from accessing them until we actually register them.

```java
public static final RegistrySupplier<Item> EXAMPLE_ITEM = ITEMS.register("example_item", () -> new Item(new Item.Properties()));
```

We can now submit our registry entries to the registry themselves, we will do this in our initialization block, please make sure that this is called only after we pass our mod event bus to architectury:

```java
ITEMS.register();
```
