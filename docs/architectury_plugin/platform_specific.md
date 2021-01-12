---
layout: page
title: Platform Specific APIs
parent: Architectury Plugin
nav_order: 1
---

# Platform Specific APIs
{: .no_toc }

---

## Don't like annotation magic? Use plain java.
Modders are not forced to use Architectury Injectables to access platform-specific APIs. You may just use something simpler, like an interface.

## Architectury Injectables

Architectury Plugin adds [Architectury Injectables](https://github.com/architectury/architectury-injectables/) to your common module.

### Disabling Architectury Injectables

Inject `injectInjectables = false` in front of `common()` in the common module architectury extension block.

### ArchitecturyTarget
Architectury Injectables provide `ArchitecturyTarget.getCurrentTarget()`, which returns the identifier of the current target, it may be (but not limited to):
- fabric
- forge

### @ExpectPlatform

`@ExpectPlatform` can be applied to **static methods**, and its content will be replaced by the platform-specific implementation.

Here we will declare a method with `@ExpectPlatform`, please note that you don't need to do this to get the configuration directory *if you are using the Architectury API*.
```java
package net.examplemod;

import me.shedaniel.architectury.annotations.ExpectPlatform;

import java.io.File;

class ExampleClass {
    @ExpectPlatform
    static File getConfigDirectory() {
        // Just throw an error, the content should get replaced at runtime.
        // Something is terribly wrong if this is not replaced.
        throw new AssertionError();
    }
}
```

Now, we can go and implement the platform-specific version of this method, we will do Fabric as an example.
The package of this class is suffixed with `.fabric`, and the name of this platform-specific class is suffixed with `Impl`.
```java
package net.examplemod.fabric;

import net.fabricmc.loader.api.FabricLoader;

import java.io.File;

public class ExampleClassImpl {
    public static File getConfigDirectory() {
        return FabricLoader.getInstance().getConfigDir().toFile();
    }
}
```
