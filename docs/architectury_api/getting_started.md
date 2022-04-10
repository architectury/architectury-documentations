---
layout: page
title: Getting Started
parent: Architectury API
nav_order: 1
---

# Getting Started
{: .no_toc }

---

Download templates from [Architectury Templates](https://github.com/architectury/architectury-templates/releases/) and import it as a Gradle project.

## I don't want Architectury API...

Remove lines related to Architectury API in each of the `build.gradle` in `common/`, `fabric/`, and `forge/`. They should look at this:
```diff
dependencies {
    // We depend on fabric loader here to use the fabric @Environment annotations and get the mixin dependencies
    // Do NOT use other classes from fabric loader
    modImplementation "net.fabricmc:fabric-loader:${rootProject.fabric_loader_version}"
    // Remove the next line if you don't want to depend on the API
-   modApi "dev.architectury:architectury:${rootProject.architectury_version}"
}
```

## I want Yarn instead...

Replace the line for the default Mojang Mappings in the root `build.gradle`, with one that references Yarn instead:

```diff
subprojects {
    apply plugin: "dev.architectury.loom"

    loom {
        silentMojangMappingsLicense()
    }

    dependencies {
        minecraft "com.mojang:minecraft:${rootProject.minecraft_version}"
-       // The following line declares the mojmap mappings, you may use other mappings as well
-       mappings loom.officialMojangMappings()
        // The following line declares the yarn mappings you may select this one as well.
-       // mappings "net.fabricmc:yarn:@YARN_MAPPINGS@:v2"
+       mappings "net.fabricmc:yarn:@YARN_MAPPINGS@:v2"
    }
}
```

