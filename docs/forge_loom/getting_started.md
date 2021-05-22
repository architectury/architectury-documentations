---
layout: page
title: Getting Started
parent: Forge Loom
nav_order: 1
---

# Getting Started

{: .no_toc }

---

## The Easy Way (100% From Scratch)
Clone the [Architectury Loom Example Mod](https://github.com/architectury/archloom-example-mod) and import build.gradle as a project.

## The Not Quite So Easy Way (Converting [Fabric Mods](https://github.com/FabricMC/fabric-example-mod) to Forge)

Within `settings.gradle`, insert the repository to Architectury Loom (as well as Forge's maven for Forge / MCP / etc.):

```diff
pluginManagement {
    repositories {
        maven { url "https://maven.fabricmc.net/" }
+       maven { url "https://maven.architectury.dev/" }
+       maven { url "https://files.minecraftforge.net/maven/" }
        gradlePluginPortal()
    }
}
```

Within `gradle.properties`, insert `loom.platform=forge`.  
Within `build.gradle`, go to the `plugins` block and replace `fabric-loom` with any version of `forgified-fabric-loom`, for example:

```diff
plugins {
-	id 'fabric-loom' version '<version>'
+	id 'dev.architectury.loom' version '0.7.2-SNAPSHOT'
	id 'maven-publish'
}
```

**NOTE:** 0.7.2-SNAPSHOT is the current recommended version.

and insert the Forge dependency in the `dependencies` block:

```groovy
dependencies {
    forge "net.minecraftforge:forge:${mc_version}-${forge_version}"
}
```

## Generating Sources

You can generate the Minecraft sources for reference (since IDEA already has a decompiler this is only useful for searching through the code):

Run the `genSources` Gradle task. If your IDE doesn't have Gradle integration, then run the following command in the terminal: `gradlew genSources` (
or `./gradlew genSources` on Unix-based systems).

## Run Configurations

### IntelliJ IDEA

Run Configurations should be automatically generated on configuration, please **DO NOT** run `gradlew idea` as it may mess up your project.

### Visual Studio Code

Run Configurations should be automatically generated on configuration, please **DO NOT** run `gradlew vscode` as it may mess up your project.

### CLI

Run `gradlew runClient` or `gradlew runServer`.
