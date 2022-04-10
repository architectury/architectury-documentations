---
layout: page
title: Using MCP
parent: Architectury Loom
---

# Using MCP
{: .no_toc }

---

**Note:** MCP is no longer used since Minecraft 1.17, and has been replaced with Official Mojang Mappings.

Experimental MCP support is available in Architectury Loom. MCP docs and parameter mappings are fully supported in Forge Loom. However, MCP will **not** work in snapshots, 
as the MCP support depends on matching the MCPConfig with your intermediary.

Declare the MCP mappings dependency as follows: (`20201028-1.16.3` is just an example version!)
```groovy
dependencies {
    mappings "de.oceanlabs.mcp:mcp_snapshot:20201028-1.16.3"
}
```

## Using Architectury Loom to remap a MCP mapped project to yarn / mojmap

After setting up a loom environment with MCP mappings, you may migrate the code to another mappings. Read the [wiki page](https://fabricmc.net/wiki/tutorial:migratemappings) for more help.

#### Migrating to MojMap:

`gradlew migrateMappings --mappings "net.mojang.minecraft:mappings:VERSION"`

#### Migrating to Yarn: (`1.16.5+build.3` is just an example yarn build!)

`gradlew migrateMappings --mappings "1.16.5+build.3"`
