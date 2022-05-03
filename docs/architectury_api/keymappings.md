---
layout: page
title: KeyMappings
parent: Architectury API
nav_order: 6
---

# KeyMappings
{: .no_toc }

---

With custom KeyMappings, clients can input from mouse and keyboards to do certain actions.

**Note:** The following code should only be executed from client.

## Registering KeyMappings

We can register `KeyMapping`s with `KeyMappingRegistry`.

First, let's create a `KeyMapping`:

```java
// A key mapping with keyboard as the default
public static final KeyMapping CUSTOM_KEYMAPPING = new KeyMapping(
    "key.examplemod.custom_key", // The translation key of the name shown in the Controls screen
    InputConstants.Type.KEYSYM, // This key mapping is for Keyboards by default
    InputConstants.KEY_P, // The default keycode
    "category.examplemod.example" // The category translation key used to categorize in the Controls screen 
);

// A key mapping with mouse as the default
public static final KeyMapping CUSTOM_KEYMAPPING = new KeyMapping(
    "key.examplemod.custom_key", // The translation key of the name shown in the Controls screen
    InputConstants.Type.MOUSE, // This key mapping is for Mouse by default
    InputConstants.MOUSE_BUTTON_LEFT, // The default button
    "category.examplemod.example" // The category translation key used to categorize in the Controls screen 
);

// A key mapping with no default
public static final KeyMapping CUSTOM_KEYMAPPING = new KeyMapping(
    "key.examplemod.custom_key", // The translation key of the name shown in the Controls screen
    InputConstants.Type.KEYSYM, // This key mapping is for Keyboards by default
    -1, // The default keycode
    "category.examplemod.example" // The category translation key used to categorize in the Controls screen 
);
```

We can register the key mapping in a method now.
```java
KeyMappingRegistry.register(CUSTOM_KEYMAPPING);
```

### Listening to when the key is pressed

We will register a client tick event, and consume the key there.

```java
ClientTickEvent.CLIENT_POST.register(minecraft -> {
	while (CUSTOM_KEYMAPPING.consumeClick()) {
        // Do action here
    }
});
```

