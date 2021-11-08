---
layout: page
title: Using Mixins
parent: Forge Loom
---

# Using Mixins
{: .no_toc }

---

As per traditional Loom fashion, Forge Loom provides excellent Mixin support out of the box.
Forge Loom also defaults into using the FabricMC's fork of Mixin for better refmap handling in development environments.

### Dependencies with Mixin

Forge Loom works with dependencies with mixin, Forge Loom injects a remapper into your development environment to properly remap srg reference maps to named.
This is all handled for you in Forge Loom, so you don't need to worry.

### Do I need MixinGradle?

No.

For a matter of fact, MixinGradle is only responsible for adding the compiler arguments for the Mixin Annotation Processor to create the refmaps.
Forge Loom uses its own [Mixin Compiler Extensions](https://github.com/FabricMC/fabric-mixin-compile-extensions) to create the refmaps, and support for it is directly added in Loom.

### Declaring Mixins

The Fabric Mod Loader uses the `fabric.mod.json` to load mixin configs, on Forge, the `MixinConfigs` argument is used instead, Loom will handle adding the arguments for you within both the development environment, and the compiled jar.

You must tell Loom what mixins you have, by declaring the following in your `build.gradle`.

```groovy
loom {
    forge {
        mixinConfig "mixin.examplemod.json"
    }
}
```
