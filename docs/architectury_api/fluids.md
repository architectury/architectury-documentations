---
layout: page
title: Fluids
parent: Architectury API
nav_order: 5
---

# Fluids
{: .no_toc }

---

## FluidStack

`FluidStack` is a platform-agnostic API of handling a `Fluid` type, `CompoundTag` nbt, and `long` amount.

The actual implementation differs with the platform, with `81000L` and `1000` being the bucket amount for Fabric and Forge respectively.

You may convert between Architectury's `FluidStack` with Forge's `FluidStack` and Fabric's `FluidVariant` with `FluidStackHooksFabric` and `FluidStackHooksForge`. Methods that convert from Architectury to platform does not do a copy, while the reverse will create a wrapper object that could be memory-intensive.

### ArchitecturyFluidAttributes

`ArchitecturyFluidAttributes` allows declaring more properties for creating and defining a fluid. Most of the methods contain nullable types, please make sure you check the null-ability often.

### SimpleArchitecturyFluidAttributes

`SimpleArchitecturyFluidAttributes` is a simple implementation of `ArchitecturyFluidAttributes` with a builder-style setup. Extending this class may be easier than extending the base interface.

#### Creating the Attributes

```java
public static final ArchitecturyFluidAttributes EXAMPLE_FLUID_ATTRIBUTES = SimpleArchitecturyFluidAttributes.ofSupplier(() -> EXAMPLE_FLUID, () -> EXAMPLE_FLUID_FLOWING);
```

`FLOW` and `SOURCE` isn't defined yet, we will define them later.

With `SimpleArchitecturyFluidAttributes`, you can define extra attributes of the fluid, such as the texture, color, temperature, or whether it can infinitely convert to source. You can read the JavaDocs of `ArchitecturyFluidAttributes`.

## Registering Fluids

#### Registrar Order

On Forge, Fluid Registry is ran **after** blocks, that is why the `LiquidBlock` constructor takes a supplier of the fluid you create afterwards. However, this isn't the same on Fabric, registering fluids should go before registering blocks.

If you are using the `DeferredRegister<?>` API to register content (see [#Registry](/docs/architectury_api/registry)), you should move `FLUIDS.register()` before `BLOCKS.register()` and `ITEMS.register()`. The order of `.register()` does not matter on Forge, but it does on Fabric where it registers immediately.

#### Creating the Fluid

```java
public static final RegistrySupplier<Fluid> EXAMPLE_FLUID = FLUIDS.register("example_fluid", () -> new ArchitecturyFlowingFluid.Source(EXAMPLE_FLUID_ATTRIBUTES));

public static final RegistrySupplier<Fluid> EXAMPLE_FLUID_FLOWING = FLUIDS.register("example_fluid_flowing", () -> new ArchitecturyFlowingFluid.Flowing(EXAMPLE_FLUID_ATTRIBUTES));
```

#### Creating the Fluid Block

```java
// Copying the fluid block properties of a water block, you can change that
public static final RegistrySupplier<LiquidBlock> EXAMPLE_FLUID_BLOCK = BLOCKS.register("example_fluid", () -> new ArchitecturyLiquidBlock(EXAMPLE_FLUID, BlockBehaviour.Properties.copy(Blocks.WATER)));
```

#### Creating the Fluid Bucket

```java
public static final RegistrySupplier<Item> EXAMPLE_FLUID_BUCKET = ITEMS.register("example_fluid_bucket", () -> new ArchitecturyBucketItem(EXAMPLE_FLUID, new Item.Properties().tab(EXAMPLE_TAB)));
```

#### Adding our blocks and buckets to the Attribute

You may find that some of these fields are not accessible because they are forward referencing, you can avoid this by qualifying the field owner class.

```java
public static final ArchitecturyFluidAttributes EXAMPLE_FLUID_ATTRIBUTES = new SimpleArchitecturyFluidAttributes(() -> ExampleRegistries.EXAMPLE_FLUID, () -> ExampleRegistries.EXAMPLE_FLUID_FLOWING)
    .blockSupplier(() -> ExampleRegistries.EXAMPLE_FLUID_BLOCK)
    .bucketItemSupplier(() -> ExampleRegistries.EXAMPLE_FLUID_BUCKET);
```

#### Adding the fluid to Tags

A lot of the logic depends on vanilla tag `#minecraft:water` and `#minecraft:lava`, you can read more on them [here](https://minecraft.fandom.com/wiki/Tag#Fluids).
