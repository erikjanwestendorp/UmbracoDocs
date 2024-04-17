---
description: Learn how to create your first extension for Umbraco.
---

# Creating your first extension

This guide will help you set up your first extension with a Web Component using two ways:

1. [Vanilla JavaScript](creating-your-first-extension.md#extension-with-vanilla-javascript) or
2. [Vite, Typescript, and Lit](creating-your-first-extension.md#extension-with-vite-typescript-and-lit)

Before following this tutorial make sure to read the [Setup Your Development Environment](../extending-backoffice/development-flow/) article.

This article is also part of the prerequisites for [Creating a Property Editor](creating-a-property-editor/) and [Creating a Custom Dashboard](creating-a-custom-dashboard.md) tutorials.

## App\_Plugins

Extensions will go into a folder called `App_Plugins`. If you don't have this folder, you can create it at the root of your Umbraco project.

## Extension with Vanilla JavaScript

We consider it best practice to use at least TypeScript and some kind of build tool to write your extensions. However, since Umbraco's extension system is written entirely in JavaScript, it's possible to create extensions with vanilla JavaScript. For the sake of posterity, we will briefly go through what that looks like:

1. Go to the `App_Plugins` folder and create a new folder called `my-vanilla-extension`
2. In the newly created folder, create a file called `umbraco-package.json`. Then add the following code :

{% code title="umbraco-package.json" lineNumbers="true" %}

```json
{
  "$schema": "../../umbraco-package-schema.json",
  "name": "My.Vanilla.Extension",
  "version": "0.1.0",
  "extensions": [
    {
      "type": "dashboard",
      "alias": "my.vanilla.extension",
      "name": "My Vanilla Extension",
      "js": "/App_Plugins/my-vanilla-extension/vanilla-extension.js",
      "weight": -1,
      "meta": {
        "label": "My Vanilla Extension",
        "pathname": "my-vanilla-extension"
      },
      "conditions": [
        {
          "alias": "Umb.Condition.SectionAlias",
          "match": "Umb.Section.Content"
        }
      ]
    }
  ]
}
```

{% endcode %}

This code sets up a basic package with a dashboard extension.

{% hint style="info" %}
Adding `$schema` to `umbraco-package.json` will give you IntelliSense for this file to help you see different options for your package.
{% endhint %}

3. Next, create a new JavaScript file called `vanilla-extension.js` and insert the following code:

{% code title="vanilla-extension.js" lineNumbers="true" %}

```javascript
import { UmbElementMixin } from "@umbraco-cms/backoffice/element-api";
import { UMB_NOTIFICATION_CONTEXT } from "@umbraco-cms/backoffice/notification";

const template = document.createElement("template");
template.innerHTML = `
  <style>
    :host {
      padding: 20px;
      display: block;
      box-sizing: border-box;
    }
  </style>

  <uui-box>
    <h1>Welcome to my dashboard</h1>
    <p>Example of vanilla JS code</p>

    <uui-button label="Click me" id="clickMe" look="secondary"></uui-button>
  </uui-box>
`;

export default class MyDashboardElement extends UmbElementMixin(HTMLElement) {
    /** @type {import('@umbraco-cms/backoffice/notification').UmbNotificationContext} */
    #notificationContext;

    constructor() {
        super();
        this.attachShadow({ mode: "open" });
        this.shadowRoot.appendChild(template.content.cloneNode(true));

        this.shadowRoot
            .getElementById("clickMe")
            .addEventListener("click", this.onClick.bind(this));

        this.consumeContext(UMB_NOTIFICATION_CONTEXT, (instance) => {
            this.#notificationContext = instance;
        });
    }

    onClick = () => {
        this.#notificationContext?.peek("positive", {
            data: { headline: "Hello" },
        });
    };
}

customElements.define("my-vanilla-extension", MyDashboardElement);
```

{% endcode %}

Now we have a JavaScript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

5. Press the F5 button in your favorite IDE or run `dotnet run` in a command line to run the project. Then you will see the new dashboard show up in the Content section.

<figure><img src="../.gitbook/assets/Create_first_extension_Vanilla (1).png" alt=""><figcaption><p>Dashboard using Vanilla JS</p></figcaption></figure>

Clicking the button will open a notification with the message "Hello".

## Extension with Vite, Typescript, and Lit

You now have a working extension with a dashboard Web Component written in plain JavaScript and no build tool. However, Umbraco recommends building extensions with a setup using TypeScript and a build tool such as [Vite](https://vitejs.dev). Umbraco uses the library [Lit](https://lit.dev) for building web components which we will be using throughout this guide.

### Getting Started With Vite

{% hint style="info" %}
If you want to learn more about Vite, you can read the [Vite Package Setup](../extending-backoffice/development-flow/vite-package-setup.md) article. It will go into more detail about the setup and how to use Vite with Umbraco. For this tutorial, we will only cover the basics and assume you have no Vite setup yet.
{% endhint %}

Vite comes with a set of really good presets to get you quickly up and running with libraries and languages. Examples: Lit, Svelte, and vanilla Web Components with both JavaScript and TypeScript. We will use their preset of Lit and TypeScript.

Find a place where you want to keep your source files, this could be a new folder under the `App_Plugins` folder.

{% hint style="info" %}
Be aware that any files in the `App_Plugins` folder are publicly available. If you want to keep your source files private, you should create a new folder outside of the `App_Plugins` folder. Your source files could be in a whole new project where you build your extension and then copy the build files to the `App_Plugins` folder.
{% endhint %}

1. In the `App_Plugins` folder paste and run the following command in your terminal:

```bash
npm create vite@latest my-typescript-extension -- --template lit-ts
```

This sets up our new project in a folder named `my-typescript-extension` and creates a `package.json` file, which includes the necessary packages.

2. Navigate to the new `my-typescript-extension` project folder and install the packages using:

```bash
npm install
```

3. The last thing we need to install now is our Backoffice package. You can install the package using the following command:

```bash
npm install --registry https://www.myget.org/F/umbracoprereleases/npm/ -D @umbraco-cms/backoffice@14.0.0-rc1
```

This will add a package to your devDependencies containing the TypeScript definitions for the Umbraco Backoffice. The `-rc1` is the version of the package, which will change as new versions are released.

{% hint style="warning" %}
If you see any errors during this process, make sure that you have the right tools installed (Node, .NET, and so on). Also, make sure you have followed the steps on how to [Setup Your Development Environment](../extending-backoffice/development-flow/).
{% endhint %}

4. At the root of the `my-typescript-extension` folder create a new file called `vite.config.ts` and insert the following code:

```javascript
import { defineConfig } from 'vite';

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

This alters the Vite default output into a "library mode", where the output is a JavaScript file with the same name as the `name` attribute in `package.json`.

{% hint style="info" %}
You can read more about [Vite's build options here](https://vitejs.dev/config/build-options.html#build-lib).
{% endhint %}

5. Navigate to `src/my-element.ts`, open the file and replace it with the following code:

{% code title="src/my-element.ts" lineNumbers="true" %}

```typescript
import {
    LitElement,
    html,
    customElement,
} from "@umbraco-cms/backoffice/external/lit";
import { UmbElementMixin } from "@umbraco-cms/backoffice/element-api";
import {
    UmbNotificationContext,
    UMB_NOTIFICATION_CONTEXT,
} from "@umbraco-cms/backoffice/notification";

@customElement("my-typescript-element")
export default class MyTypeScriptElement extends UmbElementMixin(LitElement) {
    #notificationContext?: UmbNotificationContext;

    constructor() {
        super();
        this.consumeContext(UMB_NOTIFICATION_CONTEXT, (_instance) => {
            this.#notificationContext = _instance;
        });
    }

    #onClick = () => {
        this.#notificationContext?.peek("positive", {
            data: { message: "#h5yr" },
        });
    };

    render() {
        return html`
            <uui-box headline="Welcome">
                <p>A TypeScript Lit Dashboard</p>
                <uui-button
                    look="primary"
                    label="Click me"
                    @click=${this.#onClick}
                ></uui-button>
            </uui-box>
        `;
    }
}

declare global {
    interface HTMLElementTagNameMap {
        "my-typescript-element": MyTypeScriptElement;
    }
}

```

{% endcode %}

{% hint style="warning" %}
If you create multiple dashboards it's necessary to change the alias of `@customElement` to a unique alias in the `my-element.ts` file. If it's not changed then it will conflict with the other dashboards that use the same alias and therefore only one will show.
{% endhint %}

The code above defines a Web Component that contains a button that when clicked will open a notification with a message to the user.

6. At the root of the `my-typescript-extension` folder build the `ts` file so we can use it in our package:

```bash
npm run build
```

After running the build, you will see a new file in the `dist` folder with the name `my-typescript-extension.js`. This is the file we will use in our package.

7. At the root of the `my-typescript-extension` folder create a `umbraco-package.json` file with the following:

{% code title="umbraco-package.json" lineNumbers="true" %}

```json
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My TypeScript Extension",
    "version": "0.1.0",
    "extensions": [
        {
            "type": "dashboard",
            "alias": "My.Dashboard.MyTypeScriptExtension",
            "name": "My TypeScript Extension",
            "js": "/App_Plugins/my-typescript-extension/dist/my-typescript-extension.js",
            "weight": -1,
            "meta": {
                "label": "My TypeScript Extension",
                "pathname": "my-typescript-extension"
            },
            "conditions": [
                {
                    "alias": "Umb.Condition.SectionAlias",
                    "match": "Umb.Section.Content"
                }
            ]
        }
    ]
}
```

{% endcode %}

Now we have a JavaScript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

8. Press the F5 button in your favorite IDE or run `dotnet run` in a command line to run the project. Then you will see the new dashboard show up in the Content section.

<figure><img src="../.gitbook/assets/Create_first_extension_Typescript (1).png" alt=""><figcaption><p>Dasboard using TypeScript</p></figcaption></figure>

Clicking the button will open a notification with the message "#h5yr".

## Next

Now that you have created your first extension (which is a dashboard), you can continue to the next tutorial: [Creating a Custom Dashboard](creating-a-custom-dashboard.md).

You can also read more about the [Umbraco Package Manifest](../extending-backoffice/package-manifest.md) to learn more about the different options you have when creating an extension.
