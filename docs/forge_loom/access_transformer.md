---
layout: page
title: Access Transformer
parent: Architectury Loom
---

# Access Transformer
{: .no_toc }

---

Access Transformers must be created in `META-INF/accesstransformer.cfg`, in MCP and SRG mappings. (Basically keep your ATs from Forge, don't remap them)

You may also refer to the [Forge Documentation](https://mcforge.readthedocs.io/en/latest/advanced/accesstransformers/) on this topic if you are new to this.

For forge code(if method above doesn't work):
```groovy
  loom {
    forge {
        accessTransformer(file('src/main/resources/META-INF/accesstransformers.cfg'))
    }
  }
```
For fabric code(if `fabric.mod.json` doesn't work): 
```groovy
  loom {
    accessWidenerPath = file("src/main/resources/accesstransformer.accesswidener")
  }
```
