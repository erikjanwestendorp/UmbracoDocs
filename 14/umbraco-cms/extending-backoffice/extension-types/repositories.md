# Repositories

{% hint style="warning" %}
This page is a work in progress. It will be updated as the software evolves.
{% endhint %}

A repository is the Backoffices entry point to request data and get notified about updates. Each domain should register their own repository in the Backoffice.

### Register a Repository <a href="#register-a-repository" id="register-a-repository"></a>

```typescript
import { umbExtensionRegistry } from '@umbraco-cms/backoffice/extension-registry';
import { MyRepository } from './MyRepository';

const repositoryManifest = {
	type: 'repository',
	alias: 'My.Repository',
	name: 'My Repository',
	api: MyRepository,
};
```

With a repository we can have different data sources depending on the state of the app. It can be from a server, an offline database, a store, a Signal-R connection, etc. That means that the consumer will not have to be concerned how to access the data, add or remove items from a collection of items, etc. This means we get a loose connection between the consumer and the data storing procedures hiding all complex implementation.

### Data flow with a repository  <a href="#data-flow-with-a-repository" id="data-flow-with-a-repository"></a>

<figure><img src="../../.gitbook/assets/data-flow.svg" alt=""><figcaption><p>Data flow</p></figcaption></figure>

A repository has to be instanced in the context where it is used. It should take a host element as part of the constructor, so any contexts consumed in the repository (notifications, modals, etc.) get rendered in the correct DOM context.

A repository can be called directly from an element, but will often be instantiated in a context, like the Workspace Context.

### The Repository Class <a href="#the-repository-class" id="the-repository-class"></a>

TODO: get typescript interface TODO: show repository example.
