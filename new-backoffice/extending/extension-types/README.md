---
description: >-
  The declaration of an extension is done by an Extension Manifest, either
  registered via an Umbraco-Package Manifest or directly to the Extension
  Registry in JavaScript.
---

# Extension Manifests

### Extension Manifest Type

Each Extension Manifest has to declare its type, this is used to determine where it hooks into the system. It also looks at what data is required to declare within it.

The pages of this article describe all the extension types that Backoffice supports. Here is a list of the most common types:

{% content-ref url="dashboards.md" %}
[dashboards.md](dashboards.md)
{% endcontent-ref %}

{% content-ref url="property-editors/" %}
[property-editors](property-editors/)
{% endcontent-ref %}

{% content-ref url="sections-and-trees.md" %}
[sections-and-trees.md](sections-and-trees.md)
{% endcontent-ref %}

## Declare Extension Manifest&#x20;

Extension Manifest and can be declared in multiple ways. One of these is to declare it as part of the [Umbraco Package Manifest](../package-manifest.md).

You can declare new Extension Manifests in JavaScript at any given point.

```typescript
import { umbExtensionsRegistry } from "@umbraco-cms/backoffice/extension-registry"

const manifest = {
    type: '...',
    ...
};

umbExtensionsRegistry.register(extension);
```

Backoffice also comes with two Extension types which can be used to register more extensions.

### Using `bundle` to declare other Extension Manifest

The bundle extension type can be used for declaring multiple Extension Manifests with JavaScript in a single file.

The bundle declares a single JavaScript file that will be loaded at startup. All the Extension Manifests exported from this Module will be registered in the Extension Registry.

\[TBD link to article on the matter].

### Using `entryPoint` as your foundation

The `entryPoint` extension type is special, it can be used to run any JavaScript code at startup.\
This can be used as an entry point for a package. \
The entry point declares a single JavaScript file that will be loaded and run when the Backoffice starts.

The `entryPoint` extension is also the way to go if you want to load in external libraries such as jQuery, Angular, React, etc. You can use the `entryPoint` to load in the external libraries to be shared by all your extensions. Loading **global CSS files** can also be used in the `entryPoint` extension.

Read more about the `entryPoint` extension type in the [Entry Point](entry-point.md) article.
