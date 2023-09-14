---
description: Learn how to create your first extension for Umbraco.
---

# Creating your first extension

This guide will help you set up your first extension using vanilla Javascript or Vite, Typescript, and Lit and is part of the prerequisites for [Creating a Property Editor](creating-a-property-editor/) and [Creating a Custom Dashboard](creating-a-custom-dashboard.md) tutorials.

## The end result:

By the end of this tutorial, we will have a simple extension up and running with a Web Component made with vanilla Javascript or made and set up with Vite, Typescript, and Lit.

{% hint style="info" %}
If you want to set up an extension with Vite, Typescript, and Lit, you can skip the section "Extension with Vanilla Javascript".
{% endhint %}

## App\_Plugins

Extensions will go into a folder called `App_Plugins`. If you don't have this folder, you can create it at the root of your Umbraco project.

## Extension with Vanilla Javascript

We consider it best practice to use at least TypeScript and some kind of build tool to write your extensions, but since Umbraco's extension system is written entirely in JavaScript, it is possible to create extensions with vanilla JavaScript. For the sake of posterity, we will briefly go through what that looks like:

Go to the `App_Plugins` folder and create a new folder called `my-package`

Navigate into the folder and create a file called `umbraco-package.json`, and paste the following code. This code sets up a basic package with a dashboard extension:

{% code title="umbraco-package.json" lineNumbers="true" %}
```json
{
	"$schema": "../../umbraco-package-schema.json",
	"name": "My.Package",
	"version": "0.1.0",
	"extensions": [
		{
			"type": "dashboard",
			"alias": "my.custom.dashboard",
			"name": "My Dashboard",
			"js": "/App_Plugins/my-package/dashboard.js",
			"weight": -1,
			"meta": {
				"label": "My Dashboard",
				"pathname": "my-dashboard"
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

{% hint style="info" %}
Adding `$schema` to `umbraco-package.json` will give you IntelliSense for this file to help you see different options for your package.
{% endhint %}

Next, create a new JavaScript file called `dashboard.js` and insert the following code:

{% code title="dashboard.js" lineNumbers="true" %}
```javascript
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api';
import { UMB_NOTIFICATION_CONTEXT_TOKEN } from '@umbraco-cms/backoffice/notification';

const template = document.createElement('template');
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
		this.attachShadow({ mode: 'open' });
		this.shadowRoot.appendChild(template.content.cloneNode(true));

		this.shadowRoot.getElementById('clickMe').addEventListener('click', this.onClick.bind(this));

		this.consumeContext(UMB_NOTIFICATION_CONTEXT_TOKEN, (_instance) => {
			this.#notificationContext = _instance;
		});
	}

	onClick = () => {
		this.#notificationContext?.peek('positive', { data: { headline: 'Hello' } });
	};
}

customElements.define('my-custom-dashboard', MyDashboardElement);
```
{% endcode %}

### Running it

Now we have a Javascript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

Press the F5 button in your favorite IDE or run `dotnet run` in a command line, and you should be able to see the new dashboard show up in the Content section.

You can read more on how to run Umbraco in the [Installation article](../fundamentals/setup/installation/).

## Extension with Vite, Typescript, and Lit

Umbraco recommends building extensions with a setup using TypeScript and a build tool such as Vite. Umbraco uses the library Lit for building web components which we will be using throughout this guide.

### Getting Started With Vite

Vite comes with a set of really good presets to get you quickly up and running with libraries and languages such as Lit, Svelte, and vanilla Web Components with both JavaScript and TypeScript. We will use their preset of Lit and TypeScript.

Find a place where you want to keep your source files and paste the following command:

```bash
npm create vite@latest -- --template lit-ts my-extension
```

This sets up our new project and creates a `package.json` file, which includes the necessary packages. Navigate to the new project folder and install the packages using:

```bash
npm install
```

The last thing we need to install now is our Backoffice package. You can install the package using the following command:

```bash
npm install -D @umbraco-cms/backoffice
```

{% hint style="warning" %}
If you see any errors during this process, make sure that you have the right tools installed (Node, .NET, and so on). Also, make sure you have followed the steps on how to [Setup Your Development Environment](../extending/development-flow.md).
{% endhint %}

Next, create a new file called `vite.config.ts` and insert the following code:

```javascript
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

This alters the Vite default output into a "library mode", where the output is a javascript file with the same name as the `name` attribute in `package.json`. The name is `my-extension` if you followed this tutorial with no changes.

{% hint style="info" %}
You can read more about [Vite's build options here](https://vitejs.dev/config/build-options.html#build-lib).
{% endhint %}

Navigate to `src/my-element.ts`, open the file and replace it with the following code:

{% code title="src/my-element.ts" lineNumbers="true" %}
```typescript
import { LitElement, html } from "lit";
import { customElement } from "lit/decorators.js";
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api';
import { UmbNotificationContext, UMB_NOTIFICATION_CONTEXT_TOKEN } from '@umbraco-cms/backoffice/notification';

@customElement('my-element')
export default class MyElement extends UmbElementMixin(LitElement) {
	private _notificationContext?: UmbNotificationContext;

	constructor() {
		super();
		this.consumeContext(UMB_NOTIFICATION_CONTEXT_TOKEN, (_instance) => {
			this._notificationContext = _instance;
		});
	}

	onClick() {
		this._notificationContext?.peek('positive', { data: { message: '#h5yr' } });
	}

	render() {
		return html`
			<uui-box headline="Welcome">
				<p>A TypeScript Lit Dashboard</p>
				<uui-button look="primary" label="Click me" @click=${() => this.onClick()}></uui-button>
			</uui-box>
		`;
	}
}

declare global {
	interface HTMLElementTagNameMap {
		'my-element': MyElement;
	}
}
```
{% endcode %}

The code above defines a Web Component that contains a button that when clicked will open a notification with a message to the user.

Next, we are going to build the `ts` file so we can use it in our package:

```bash
npm run build
```

After running build, you will see a new file in the `dist` folder with the name `my-extension.js`. Copy this file and navigate to `App_Plugins` in your Umbraco project, and create a new folder called `my-package`. Here we are going to insert the copied file.

Finally, add a file called `umbraco-package.json` the root of the folder`my-package`and insert the following code:

{% code title="umbraco-package.json" lineNumbers="true" %}
```json
{
	"$schema": "../../umbraco-package-schema.json",
	"name": "My.Package",
	"version": "0.1.0",
	"extensions": [
		{
			"type": "dashboard",
			"alias": "my.custom.dashboard",
			"name": "My Dashboard",
			"js": "/App_Plugins/my-package/my-extension.js",
			"weight": -1,
			"meta": {
				"label": "My Dashboard",
				"pathname": "my-dashboard"
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

### Running it

Now we have a Javascript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

Press the F5 button in your favorite IDE or run `dotnet run` in a command line, and you should be able to see the new dashboard show up in the Content section.

You can read more on how to run Umbraco in the [Installation article](../fundamentals/setup/installation/).
