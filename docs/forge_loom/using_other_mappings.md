---
layout: page
title: Using Non-MojMap Mappings
parent: Forge Loom
---

# Using Non-MojMap Mappings
{: .no_toc }

---

Non-MojMap mappings may not work well with the default Mixin reference remapper.
We will want to switch to using [FabricMC's fork of Mixin](https://www.github.com/FabricMC/Mixin) to enable advanced APIs for Forge Loom to remap.

Switch to [FabricMC's fork of Mixin](https://www.github.com/FabricMC/Mixin) by declaring such in the loom extension block.
```groovy
loom {
  useFabricMixin = true
}
```
