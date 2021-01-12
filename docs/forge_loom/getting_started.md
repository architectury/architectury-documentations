---
layout: page
title: Getting Started
parent: Forge Loom
nav_order: 1
---

# Getting Started
{: .no_toc }

---

Clone the [Fabric Example Mod](https://github.com/FabricMC/fabric-example-mod/) and import build.gradle as a project.

## Converting the project to Forge
Within `gradle.properties`, insert `loom.forge=true`.  
Within `build.gradle`, insert the Forge dependency:
```groovy
dependencies {
    forge "net.minecraftforge:forge:${mc_version}-${forge_version}"
}
```

## Generating Sources

You can generate the Minecraft sources for reference (since IDEA already has a decompiler this is only useful for searching through the code):

Run the `genSources` Gradle task. If your IDE doesn't have Gradle integration, then run the following command in the terminal: `gradlew genSources` (or `./gradlew genSources` on Unix-based systems).