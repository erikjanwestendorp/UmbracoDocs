---
description: Make reactivity with Umbraco States
---

# States

Umbraco States enables you to create [Observables](states.md#observables) based on a State. The Observables can then be observed, and when a change to the State occurs, all observers of Observables will be triggered.

### State types

Umbraco comes with a State type for the most common types of data:

* Array State
* Boolean State
* Class State
* Number State
* Object State
* String State

### Observables

\[TBD: Describe Observable]

### Observe a state via Umbraco Element or Umbraco Controller

The Umbraco Element or Controllers comes with the ability to observe an Observable.

While observing all changes will result in the callback being executed.

The example below creates a State and then turns the whole state into an Observable, which then can be observed.

<pre class="language-typescript"><code class="lang-typescript">import { UmbArrayState } from '@umbraco-cms/backoffice/observable-api';
<strong>
</strong><strong>...
</strong><strong>
</strong><strong>this.#selectionState = UmbArrayState&#x3C;string>(['item1', 'item2']);
</strong>this.selection = this.#selectionState.asObservable();
<strong>
</strong><strong>this.observe(
</strong>	this.selection,
	(selection) => {
		// This call will be executed initially and on each change of the state
	}
);
</code></pre>

### Observe part of a state

With the `asObservablePart` method, you can set up an Observable that provides a transformed outcome, based on the State.

<pre class="language-typescript"><code class="lang-typescript">this.selectionLength = this.#selectionState.asObservablePart(data => data.length);
<strong>
</strong><strong>this.observe(
</strong>	this.selectionLength,
	(length) => {
		// This call will be executed, initially and on each change of the state
		console.log("Length of selection is now ", length)
	}
);
</code></pre>

In the above example, the \`asObservablePart\` mapping function will be executed every time there is a change to the State. If the result of the method is different than before it will trigger an update to its observers.
