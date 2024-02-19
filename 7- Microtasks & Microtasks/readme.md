# Microtasks and Macrotasks in JavaScript Event Loop

Microtasks and macrotasks are two types of tasks that are executed in the JavaScript event loop. The event loop is a mechanism that handles asynchronous operations and callbacks in JavaScript.

## Microtasks:
A microtask is a small and quick task that runs after the current script or function but before returning control to the event loop. Microtasks are often used for things that need to be done as soon as possible, such as promise callbacks, mutation observer callbacks, or `queueMicrotask` functions.

## Macrotasks:
A macrotask is a larger and longer task that runs when the event loop is not busy with other tasks. Macrotasks are usually scheduled for things that are not urgent, such as `setTimeout`, `setInterval`, `setImmediate`, `requestAnimationFrame`, or I/O operations.

## Order of Processing:
1. Execute the current script or function.
2. Execute all the microtasks in the microtask queue until it is empty.
3. Render the changes to the DOM if needed.
4. Pick the oldest macrotask from the macrotask queue and execute it.
5. Go back to step 2.

This means that microtasks have a higher priority than macrotasks, and they can delay the execution of macrotasks until the microtask queue is empty. This can improve the user experience by ensuring a consistent and fast execution of tasks.

### Example:
```javascript
console.log('script start'); // macrotask 1

setTimeout(() => {
  console.log('setTimeout'); // macrotask 2
}, 0);

Promise.resolve().then(() => {
  console.log('promise 1'); // microtask 1
}).then(() => {
  console.log('promise 2'); // microtask 2
});

console.log('script end'); // macrotask 1

Output:

arduino

script start
script end
promise 1
promise 2
setTimeout

In React, microtasks and macrotasks are also relevant for understanding how the event loop works.
React and Event Loop:

React uses a scheduler to prioritize and batch updates to the UI, based on the available time and the urgency of the tasks. React also uses a concept called fiber to represent a unit of work that can be paused, resumed, or aborted by the scheduler.

React updates are usually triggered by events, such as user interactions, network requests, or timers. These events are handled by the browser as macrotasks, and they can enqueue other macrotasks or microtasks.
React Updates:

React updates are also considered as macrotasks, and they are scheduled by the React scheduler using requestIdleCallback or setTimeout.
Render and Commit Phases:

When React updates the UI, it performs two phases: render and commit. The render phase is where React calculates the changes to the UI, such as creating or updating fibers, and it can be interrupted by the scheduler if there are other higher-priority tasks. The commit phase is where React applies the changes to the UI, such as adding or removing DOM nodes, and it cannot be interrupted by the scheduler. The commit phase is also where React executes the lifecycle methods and the effects.
Microtasks in React:

Microtasks are also involved in React updates, especially when using promises or async/await. For example, when a component uses setState inside a promise callback, the state update is enqueued as a microtask, and it will be processed before the next macrotask. This means that the state update will be batched with other state updates that happen in the same event loop cycle, and React will only render once for all the state updates.
Example in React:

javascript

import React, { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("effect");
  });

  console.log("render");

  return (
    <div className="App">
      <h1>{count}</h1>
      <button
        onClick={() => {
          console.log("click");
          setCount(count + 1); // macrotask
          Promise.resolve().then(() => {
            console.log("promise");
            setCount(count + 1); // microtask
          });
        }}
      >
        Increment
      </button>
    </div>
  );
}

export default App;

Output:

arduino

render
effect
click
promise
render
effect