---
description: Get started with a Vite Package, setup with TypeScript and Lit
---

# Vite Package Setup

Umbraco recommends building extensions with a setup using TypeScript and a build tool such as Vite. Umbraco uses the library Lit for building web components which we will be using throughout this guide.

### Getting Started With Vite

Vite comes with a set of really good presets to get you quickly up and running with libraries and languages. For example: Lit, Svelte, and Vanilla Web Components with both JavaScript and TypeScript.

Create a folder in `/App_Plugins` and run the following command in that folder:

```bash
npm create vite@latest
```

This Guide will help you set up your new package, asking you to pick a framework and a compiler. We recommend **Lit** and **TypeScript**.

This sets up our new project and creates a `package.json` file, which includes the necessary packages.

Navigate to the new project folder and install the packages using:

```bash
npm install
```

The last thing we need to install now is our Backoffice package. You can install the package using the following command:

```bash
npm install -D @umbraco-cms/backoffice@14.0.0--preview003
```

{% hint style="info" %}
The `--preview003` is required to install the correct version of the package. You have to specify the specific version. Otherwise you will get the latest version of the package, which may not be compatible with the version of Umbraco you are using.
{% endhint %}

This will add a package to your devDependencies containing the TypeScript definitions for the Umbraco Backoffice.

{% hint style="warning" %}
If you see any errors during this process, make sure that you have the right tools installed (Node, .NET, and so on). Also, make sure you have followed the steps on how to [Setup Your Development Environment](./).
{% endhint %}

Next, create a new file called `vite.config.ts` and insert the following code:

```ts
import { defineConfig } from "vite";

export default defineConfig({
    build: {
        lib: {
            entry: "src/my-element.ts", // your web component source file
            formats: ["es"],
        },
        outDir: "dist", // your web component will be saved in this location
        sourcemap: true,
        rollupOptions: {
            external: [/^@umbraco/],
        },
    },
});
```

This alters the Vite default output into a **library mode**, where the output is a JavaScript file with the same name as the `name` attribute in `package.json`. The name is `my-extension` if you followed this tutorial with no changes.

{% hint style="info" %}
The `build:lib:entry` parameter can accept an array which will allow you to export multiple files during the build. You can read more about [Vite's build options here](https://vitejs.dev/config/build-options.html#build-lib).
{% endhint %}

#### Build Package

Next, we are going to build the `ts` file so we can use it in our package:

```bash
npm run build
```

### Watch for changes and build

If you like to continuously work on the package and have each change built, you can change the `dev` script of your `package.json` to `vite build --watch`.
The example below indicates where in the structure this change should be implemented:

{% code title="package.json" lineNumbers="true" %}
```json
{
  "name": "my-package",
  ...
  "scripts": {
    "dev": "vite build --watch",
    ...
  },
  ...
```
{% endcode %}

### Umbraco Package declaration

Declare your package to Umbraco, via a file called `umbraco-package.json.` This should be added at the root of your package.

This example declares a Dashboard as part of your Package, using the Vite example element.

[Learn about the abilities of the Umbraco Package here.](../package-manifest.md)

{% code title="umbraco-package.json" lineNumbers="true" %}

```json
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Package",
    "version": "0.1.0",
    "extensions": [
        {
            "type": "dashboard",
            "alias": "My.Dashboard.MyExtension",
            "name": "My Dashboard",
            "js": "/App_Plugins/my-package/dist/my-extension.js",
            "meta": {
                "label": "My Dashboard",
                "pathname": "my-dashboard"
            }
        }
    ]
}
```

{% endcode %}

### Summary

With this, you have setup your Package and created your a Extension to Backoffice.

This Dashboard will appear on all sections, so please continue by following the tutorial on [Creating A Custom Dashboard](../../tutorials/creating-a-custom-dashboard.md)
