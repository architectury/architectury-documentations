---
layout: page
title: Fixing ForgeGradle Mixin refmaps
parent: Forge Loom

---

# Fixing ForgeGradle Mixin refmaps

{: .no_toc }

---

**TL;DR: Follow the following [GitHub comment](https://github.com/SpongePowered/Mixin/issues/462#issuecomment-791370319).**

The following applies to FG3 and sub-sequence versions if there are no fixes regarding this issue.

### Addressing some misconceptions

Setting the property `mixin.env.disableRefMap` is **not** a proper fix, it may work for projects *with the same mappings*, as you are expecting that the original source of the mixin files to be in the same mappings as your development environment, which is false for some projects. (And is extremely unstable, will even break if you have a different MCP version.)

### Alternative Solutions

Specifying `mixin.env.refMapRemappingFile` or providing `net.minecraftforge.gradle.GradleStart.srg.srg-mcp` may be an alternative fix.

