---
layout: page
title: ExpectPlatform Annotation
parent: Architectury Plugin
nav_order: 2
---

# ExpectPlatform Annotation
{: .no_toc }

---

`@ExpectPlatform` can be applied to **static methods**, and its content will be replaced by the platform-specific implementation.

Here we will declare a method with `@ExpectPlatform`, please note that you don't need to do this to get the configuration directory *if you are using the Architectury API*.
```java
package net.examplemod;

import dev.architectury.injectables.annotations.ExpectPlatform;

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
