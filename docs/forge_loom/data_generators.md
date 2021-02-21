---
layout: page
title: Data Generators
parent: Forge Loom
---

# Data Generators
{: .no_toc }

---

Data Generators Support has been added to Forge Loom, starting from 0.6.55, this is how you declare it:
```groovy
loom {
    dataGen {
        mod "YOUR MODID HERE"
    }
}
```

Run `runData` or use your IDE's run configurations to generate the assets, should be the same as ForgeGradle.

Forge Loom automatically adds the following arguments: `--all --mod <the mod ids> --output <path to src/generated/resources>`, if you wish to add more (like `--existing`), following is an example on how to add additional arguments:
```groovy
loom {
    launches {
        data {
            arg "--existing", file("src/main/resources").absolutePath
        }
    }
}
```

**NOTE:** Data Generators are still in development for architectury / fabric projects, this is **only** for Forge projects!
