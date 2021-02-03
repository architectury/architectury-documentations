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

Within `settings.gradle`, insert the repository to Forge Loom:

```diff
pluginManagement {
    repositories {
        jcenter()
        maven { url "https://maven.fabricmc.net/" }
+       maven { url "https://dl.bintray.com/shedaniel/cloth" }
+       maven { url "https://files.minecraftforge.net/maven/" }
        gradlePluginPortal()
    }
}
```

Within `gradle.properties`, insert `loom.forge=true`.  
Within `build.gradle`, go to the `plugins` block and replace `fabric-loom` with any version of `forgified-fabric-loom`, for example:

```diff
plugins {
-	id 'fabric-loom' version '0.5-SNAPSHOT'
+	id 'forgified-fabric-loom' version '0.6.60'
	id 'maven-publish'
}
```

**NOTE:** 0.6.60 is not the latest version, check the latest version here: [ ![Download](https://api.bintray.com/packages/shedaniel/cloth/forgified-fabric-loom/images/download.svg) ](https://bintray.com/shedaniel/cloth/forgified-fabric-loom/_latestVersion)

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
