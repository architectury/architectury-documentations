---
layout: page
title: Using Common Mixins
parent: Architectury Plugin
---

# Using Common Mixins
{: .no_toc }

---

**NOTE:** Make sure that the common mixin json name is unique!

### Declaring Common Mixins on Fabric

Declare the mixin json path in `fabric/src/main/resources/fabric.mod.json`.

### Declaring Common Mixins on Forge

Declaring the following in your `forge/build.gradle`.

```groovy
loom {
    forge {
        mixinConfig "mixin.examplemod-common.json"
    }
}
```

