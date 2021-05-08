---
layout: page
title: Changing Log Level
parent: Forge Loom

---

# Changing Log Level

{: .no_toc }

---

Property `fabric.log.level` (Defaulted **info**) is used for managing the log level to SOUT.

You can override this property by declaring the following:

```groovy
loom {
    launches {
        client {
            property "fabric.log.level", "debug"
        }
        server {
            property "fabric.log.level", "debug"
        }
    }
}
`
```

