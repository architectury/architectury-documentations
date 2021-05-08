---
layout: page
title: Platform Specific APIs
parent: Architectury Plugin
nav_order: 1
---

# Platform Specific APIs
{: .no_toc }

---

## Don't like annotation magic? Use plain java.
Modders are not forced to use Architectury Injectables to access platform-specific APIs. You may just use something simpler, like an interface.

## Architectury Injectables

Architectury Plugin adds [Architectury Injectables](https://github.com/architectury/architectury-injectables/) to your common module.

### Disabling Architectury Injectables

Inject `injectInjectables = false` in front of `common()` in the common module architectury extension block.

### ArchitecturyTarget
Architectury Injectables provide `ArchitecturyTarget.getCurrentTarget()`, which returns the identifier of the current target, it may be (but not limited to):
- fabric
- forge

### Expect Platform

View more at [@ExpectPlatform](/docs/architectury_plugin/expect_platform).

