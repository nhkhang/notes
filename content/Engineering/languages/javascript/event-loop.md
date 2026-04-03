---
title: Event Loop
tags:
  - js
---
- Endless loop for Javacsript engine to execute work unit
	- cycle: wait -> pick -> execute
- Different type of tasks (ranked by priority)
	- microtask (async)
		- immediately after sync code and before browser render / macrotask
		- `Promise.then/catch/finally`, `MutationObserver`, `queueMicrotask()`
	- macrotask (async)
		- low priority task
		- `setTimeout`, `setInterval`, `setImmediate`
- Order flow
	- Exec sync code
	- Run all microtask, one by one until queue is empty
	- Render (opt.)
	- Run one macrotask
	- Repeat

example
```javascript
setTimeout(() => alert("timeout"));

Promise.resolve()
  .then(() => alert("promise"));

alert("code");
```
1. `code` shows first, because it’s a regular synchronous call.
2. `promise` shows second, because `.then` passes through the microtask queue, and runs after the current code.
3. `timeout` shows last, because it’s a macrotask.

**Why it matters**
- adding microtasks endlessly will freeze the page from rendering + move to next macrotask